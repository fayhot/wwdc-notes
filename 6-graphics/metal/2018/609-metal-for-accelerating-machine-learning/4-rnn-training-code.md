## [RNN Training - code](4-rnn-training-code.md)






### Example: Create a LSTM Layer for Training

```swift
// Example: Create a LSTM Layer for Training
// Create a LSTM layer descriptor
// Initialize descriptor with initial training parameters, using data source providers
// Descriptor setup is exactly the same as for inference
let descriptor = MPSLSTMDescriptor()
descriptor.useFloat32Weights = true

// Create a LSTM layer for training
let trainingWeights: NSMutableArray = [] // matrices to hold training parameters
let weightGradients: NSMutableArray = [] // matrices to hold gradients
let trainingLayer = MPSRNNMatrixTrainingLayer(
    device: device!,
    rnnDescriptor: descriptor,
    trainableWeights: trainingWeights)

trainingLayer.createWeightGradientMatrices(weightGradients,
    dataType: .float32)
```

### Example: Prepare Inputs and Outputs for Training a LSTM

```swift
// Example: Prepare Inputs and Outputs for Training a LSTM
// Create 20 matrices to hold input and output sequences for forward and gradient passes
var inputSequence: [MPSMatrix] = []
var outputSequence: [MPSMatrix] = []
var inputGradientSequence: [MPSMatrix] = []
var outputGradientSequence: [MPSMatrix] = []
for i in 0..< 20 {
// Matrix size is (1, inputSize), inputSize is number of columns
inputSequence.append(MPSMatrix(...))
// Initialize matrices for the other sequences
...
}
```

### Example: Train Activity Classifier Network with MPS

```swift
// Example: Train Activity Classifier Network with MPS
// Run CNN kernels in forward pass
let trainingStates: NSMutableArray = [] // States pass data from forward to gradient pass
// Run sequence of 20 matrices through LSTM training layer (forward pass)
trainingLayer.encodeForwardSequence(
    commandBuffer: commandBuffer,
    sourceMatrices: inputSequence,
    destinationMatrices: outputSequence,
    trainingStates: trainingStates,
    weights: trainingWeights)
// Run additional CNN kernels in forward pass
// Compute Loss
```

### Data Converters
Image to/from matrix

```swift
let imageToMatrix = MPSImageCopyToMatrix(device: device,
    dataLayout: .featureChannelsxHeightxWidth)
imageToMatrix.encodeBatch(
    commandBuffer: commandBuffer,
    sourceImages: [image1, image2],
    destinationMatrix: matrix)
```

```swift
let matrixToImage = MPSMatrixCopyToImage(
      device: device,
      dataLayout: .featureChannelsxHeightxWidth)
matrixToImage.encodeBatch(
    commandBuffer: commandBuffer,
    sourceMatrix: matrix,
    destinationImages: [image1, image2])
```
