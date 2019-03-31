# 5-mps-cnn-layers.md


## Convolution Layer


### Definition

- Core building block
- Recognizes features in input

### How it works


16 filters  5x5
                1-channel input  40x40
16-channel output  40x40



// Convolution Layer
### // Code

```swift
let convDesc = MPSCNNConvolutionDescriptor(
    kernelWidth: 5, kernelHeight: 5,
    inputFeatureChannels: 3, outputFeatureChannels: 16, 
    neuronFilter: nil)

var conv = MPSCNNConvolution(
    device: device, 
    convolutionDescriptor: convDesc,
    kernelWeights: featureFilters, 
    biasTerms: convBias, 
    flags: MPSCNNConvolutionFlags.none)
```

## Pooling Layer

### Definition

- Reduces spatial size
- Condenses information in a region of an image
- Pooling operations
  - Maximum
  - Average

```swift
var pool = MPSCNNPoolingMax(
    device: device, 
    kernelWidth: 2, kernelHeight: 2,
    strideInPixelsX: 2, strideInPixelsY: 2)
```


## Fully-Connected Layer

### Definition

- Convolution layer, where filter size == input size


```swift

let fcDesc = MPSCNNConvolutionDescriptor(
    kernelWidth: inputWidth, kernelHeight: inputHeight,
    inputFeatureChannels: 256, outputFeatureChannels: 1)

var fc = MPSCNNFullyConnected(
    device: device, 
    convolutionDescriptor: fcDesc,
    kernelWeights: fcFeatureFilters, biasTerms: fcBias, 
    flags: MPSCNNConvolutionFlags.none)
```


## Additional Layers

Neuron SoftMax Normalization


MPSImage
What is it?


```swift
let imgDesc = MPSImageDescriptor(
    channelFormat: MPSImageFeatureChannelFormat.float16,
    width: width, height: height, featureChannels: 32)

var img = MPSImage(device: device, imageDescriptor: imgDesc)
```

Batch processing

```swift
let imgDesc = MPSImageDescriptor(
    channelFormat: MPSImageFeatureChannelFormat.float16,
    width: width, height: height, featureChannels: 32 numberOfImages: 100)
var img = MPSImage(device: device, imageDescriptor: imgDesc)
```



## Detecting a Smile
Inference


```swift
 // Code Sample: Detecting a Smile Using CNN
 // Create layers
var conv1, conv2, conv3, conv4: MPSCNNConvolution
let conv1Desc = MPSCNNConvolutionDescriptor(kernelWidth: 5, kernelHeight: 5,
inputFeatureChannels: 3, outputFeatureChannels: 16, neuronFilter: nil)
conv1 = MPSCNNConvolution(device: device, convolutionDescriptor: conv1Desc,
   kernelWeights: conv1Filters, biasTerms: conv1Bias, flags: MPSCNNConvolutionFlags.none)
...
var pool: MPSCNNPoolingMax
pool = MPSCNNPoolingMax(device: device, kernelWidth: 2, kernelHeight: 2,
   strideInPixelsX: 2, strideInPixelsY: 2)
var fc1, fc2: MPSCNNFullyConnected
let fc1Desc = MPSCNNConvolutionDescriptor(kernelWidth: 2, kernelHeight: 2,
inputFeatureChannels: 64, outputFeatureChannels: 256, neuronFilter: nil)
conv1 = MPSCNNFullyConnected(device: device, convolutionDescriptor: fc1Desc,
   kernelWeights: fc1Feature, biasTerms: fc1Bias, flags: MPSCNNConvolutionFlags.none)
...
```




Object Recognition
Inference
Convolution Pooling (Avg.) Pooling (Max.) Fully-Connected SoftMax
     


Demo
Object recognition



## Memory Savings with MPSTemporaryImages

Object recognition

- 74 MPSImages (83.8MB) needed for intermediate images
- Replaced MPSImages with MPSTemporaryImages
  - Reduced CPU cost: time and energy
  - Automatic reduction of 74 images to five underlying allocations (20.5MB)
  - 76% Memory savings!

