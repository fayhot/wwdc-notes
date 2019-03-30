# [Training a Neural Network with MPS](2-cnn-training-code.md)

- Create training graph
- Prepare inputs
- Specify weights
- Execute graph
  - Graph updates weights
- Complete training process | | p105


## Step 1: Create training graph


- Describe neural network using graph API
- Image nodes—Data
- Filter nodes—Operations


```swift
let inputImage = MPSNNImageNode(handle: nil)
let conv = MPSCNNConvolutionNode(source: inputImage,
  weights: MyWeights(withFile:“conv.dat”))
let convGradient = conv.gradientFilter(source: previousNode.resultImage)
```

## Step 2: Prepare Inputs

- Inputs to the graph
  - Batch of source images
  - Batch of source states

```swift
// Encode a batch of images for training
trainingGraph.encodeBatch(
  to: commandBuffer!,
  sourceImages: [imageBatch],
  sourceStates: [statesBatch])
```

### Batches

- Batches are arrays of images or states
  - [`MPSImageBatch`](https://developer.apple.com/documentation/metalperformanceshaders/mpsimagebatch)
  - [`MPSStateBatch`](https://developer.apple.com/documentation/metalperformanceshaders/mpsstatebatch)


```swift
// Create an input image
let inputImage0 = MPSImage(texture: texture0, featureChannels: 4)
...
// Create a batch of input images
var imageBatch : [MPSImage] = []
imageBatch.append(inputImage0)
...
```

### States

- `MPSState` passes state of forward node to gradient node
- Graph manages all states

### Loss Labels

```swift
// Create one label for Loss computation
let labelData = . . . // Load label data
let labelDesc = MPSCNNLossDataDescriptor(
  data: Data(bytes: labelData),
  layout: .featureChannelsxHeightxWidth,
  size: MTLSize(width: 1, height: 1, depth: 10))!
let cnnLabel = MPSCNNLossLabels(device: device, labelsDescriptor: labelDesc)
```

### Step 3: Specify weights

#### Data Source Providers

- Convolution
- Fully Connected
- Batch normalization
- Instance normalization

```swift
// User implements MPSCNNConvolutionDataSource protocol
let conv = MPSCNNConvolutionNode(source: MPSNNImageNode(handle: nil), weights: MyWeights(withFile:“conv.dat”))
```

- Just-in-time loading and purging of weights data
- Minimize memory footprint

```swift
class MyWeights: NSObject, MPSCNNConvolutionDataSource {
init(file: String) {...} // Initialize the data source object
func load() -> Bool {...} // Graph calls load when weights for this layer are needed func descriptor() -> MPSCNNConvolutionDescriptor {...}
func weights() -> UnsafeMutableRawPointer {...}
func purge() {...} // When purge is called, you can release weights
}
```

### Step 4: Execute graph

```swift
// Example: Prepare to Execute Graph on the GPU
// Metal setup
let device = MTLCreateSystemDefaultDevice()
// Initialize graph
let trainingGraph = MPSNNGraph(device: device!, resultImage: makeTrainingGraph())
 // Prepare inputs
 ...
 // Train network on the GPU
 ...
 ```
---

```swift
// Example: Execute Graph in a Training Loop with Double Buffering
let latestCommandBuffer = nil
// NUM_EPOCHS is the number of times we iterate over an entire dataset
// NUM_ITERATIONS_PER_EPOCH is the number of images in a dataset, divided by batch size
for i in 0..<NUM_EPOCHS {
  for j in 0..<NUM_ITERATIONS_PER_EPOCH {
    latestCommandBuffer = trainingIteration(i * NUM_ITERATIONS_PER_EPOCH + j);
  }
...
}
```

---

```swift
// Example: Execute Graph in a Training Loop with Double Buffering
let doubleBufferSemaphore = DispatchSemaphore(value: 2)

func trainingIteration(_ iter: Int) -> MTLCommandBuffer {
  doubleBufferSemaphore.wait(timeout: .distantFuture)
  let commandBuffer = commandQueue.makeCommandBuffer()!
  // Encode a batch of images for training
  var outputBatch = trainingGraph.encodeBatch(to: commandBuffer,
    sourceImages: [dataset.nextImageBatch(iter)],
    sourceStates: [dataset.nextLabelsBatch(iter)])

  commandBuffer.addCompletedHandler { commandBuffer in
    // Callback is called when GPU is done executing the graph (outputBatch is ready)
    doubleBufferSemaphore.signal()
  }

  commandBuffer.commit()
  return commandBuffer
}
```

## Step 4.1: Graph updates weights


- Implement optional update method on Data Source Provider
- Graph calls update method automatically

```swift
class MyWeights: NSObject, MPSCNNConvolutionDataSource { ...
  func update(with commandBuffer: MTLCommandBuffer,
    gradientState: MPSCNNConvolutionGradientState,
    sourceState: MPSCNNConvolutionWeightsAndBiasesState)
    -> MPSCNNConvolutionWeightsAndBiasesState? {...} // GPU
}
```


### Optimizers - For updating weights

- Describe how to take update step on training parameters
- Used in update method of Data Source Provider
- Variants
  - MPSNNOptimizerAdam
  - MPSNNOptimizerStochasticGradientDescent
  - MPSNNOptimizerRMSProp
- Custom

```swift
// Example: Use an Optimizer to Update Weights
// Add an optimizer to the init method of a Data Source Provider
init(kernelWidth: Int,
  kernelHeight: Int,
  inputFeatureChannels: Int,
  outputFeatureChannels: Int) {

  let length = kernelWidth * kernelHeight * inputFeatureChannels * outputFeatureChannels
  self.optimizer = MPSNNOptimizerStochasticGradientDescent(device: device,
      learningRate: 0.01)
}
```

---

```swift
// Example: Use an Optimizer to Update Weights
func update(with commandBuffer: MTLCommandBuffer,
  gradientState: MPSCNNConvolutionGradientState,
  sourceState: MPSCNNConvolutionWeightsAndBiasesState)
  -> MPSCNNConvolutionWeightsAndBiasesState? {

    optimizer.encode(commandBuffer: commandBuffer,
      convolutionGradientState: gradientState,
      convolutionSourceState: sourceState,
      inputMomentumVectors: nil,
      resultState: sourceState)

    return sourceState
}
```

### Step 5: Complete training process

```swift

// Example: Training Loop with Double Buffering
let latestCommandBuffer = nil
// NUM_EPOCHS is the number of times we iterate over an entire dataset
// NUM_ITERATIONS_PER_EPOCH is the number of images in a dataset, divided by batch size
for i in 0..<NUM_EPOCHS {
  for j in 0..<NUM_ITERATIONS_PER_EPOCH {
    latestCommandBuffer = trainingIteration(i * NUM_ITERATIONS_PER_EPOCH + j);
  }

  // Optional steps after each epoch:
  latestCommandBuffer.waitUntilCompleted()
  // Run inference with current trained parameters on a test set
  // Optionally, stop training when the network reaches an acceptable level of accuracy
}

```
