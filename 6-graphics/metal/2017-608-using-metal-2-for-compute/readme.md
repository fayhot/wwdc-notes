# [2017 608 Using Metal 2 for Compute](https://developer.apple.com/videos/play/wwdc2017/608/)

Metal Performance Shaders (MPS) provides a highly tuned library of functions that extend the power of the GPU for more than just graphics. With Metal 2, MPS comes to the Mac along with an expanded set of capabilities. Learn how to tap into the latest image processing operations, perform linear algebra operations, and accelerate machine learning algorithms via new primitives and a graph API to build and execute neural networks on the GPU.


3924

- Metal API and language
- GPU Tools
- MetalKit
- Metal Performance Shaders

## Image Processing

- Convolution Gaussian Blur
- Box, Tent
- Sobel
- Morphology Lanczos Resampling Histogram
- Equalization and Specification Median
- Thresholding
- Transpose
- Image Integral Color Conversion Gaussian Pyramid

---


New primitives
- Image Keypoints Bilinear Rescale Image Statistics
- Element-wise Arithmetic Operations
- With broadcasting


## [Linear Algebra](1-linear-algebra.md) | |


## Machine Learning | 715 | p30


Training and Inference


- Recap on Convolutional Neural Networks (CNN)
- Convolutional Neural Networks — New Primitives | 1320
- Neural Network Graph API | 1930
- Recurrent Neural Networks (RNN) | 2720



## Recurrent Neural Networks (RNN)

```swift
// Example: Creating a LSTM RNN
// Create a LSTM layer descriptor
let descriptor = MPSLSTMDescriptor()
descriptor.inputFeatureChannels = inputSize
descriptor.outputFeatureChannels = outputSize
// Create and initialize gate weights with trained parameters, using a data source provider
// for just-in-time loading and purging of weights
descriptor.forgetGateInputWeights = MyWeights(f
descriptor.cellGateInputWeights = MyWeights(
// Initialize the rest of the gates...
ile:“forgetGateWeights.dat”)) file:“cellGateWeights.dat”))
// Metal setup
let device = MTLCreateSystemDefaultDevice()! // Also get commandQueue and commandBuffer
// Create a LSTM layer
let layer = MPSRNNMatrixInferenceLayer(device: device, rnnDescriptor: descriptor)
```
