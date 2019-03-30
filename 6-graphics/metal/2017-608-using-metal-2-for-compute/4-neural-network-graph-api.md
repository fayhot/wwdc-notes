## [Neural Network Graph API](4-neural-network-graph-api.md) | 1930 | p100


Neural Network Graph API
Overview
Describe neural network using graph API Filter nodes — Operations
Image nodes — Data



Ease of use
Compact representation
Save and restore across platforms (NSSecureCoding)
Initialize once, reuse
Execute graph on GPU with single call
No intermediate images to manage, just input/output
Auto-configuration of image sizes, padding, centering MetalImageRecognition code sample* — 4x less code with NN Graph API

Deliver best performance
Easy to parallelize between CPU and GPU Fuse graph nodes
Execute graph nodes concurrently Optimize away Concatenation nodes

```swift
func makeGraph() -> MPSNNImageNode {
let conv1 = MPSCNNConvolutionNode(source: MPSNNImageNode(handle: nil), weights: MyWeights(file:“conv1.dat”))
let pool1 = MPSCNNPoolingMaxNode(source: conv1.resultImage, filterSize: 2)
let conv2 = MPSCNNConvolutionNode(source: pool1.resultImage, weights : MyWeights(file:“conv2.dat”))
let pool2 = MPSCNNPoolingMaxNode(source: conv2.resultImage, filterSize: 2)
let conv3 = MPSCNNConvolutionNode(source: pool2.resultImage, weights: MyWeights(file:“conv3.dat”))
let pool3 = MPSCNNPoolingMaxNode(source: conv3.resultImage, filterSize: 2)
let conv4 = MPSCNNConvolutionNode(source: pool3.resultImage, weights: MyWeights(file:“conv4.dat”))
let fc1 = MPSCNNFullyConnectedNode(source: conv4.resultImage, weights: MyWeights(file:“fc1.dat”))
let fc2 = MPSCNNFullyConnectedNode(source: fc1.resultImage,     weights:MyWeights(file:“fc2.dat”))
return   fc2.resultImage
}
```



### // Example: execute graph on the GPU

```swift
// Metal setup
let device = MTLCreateSystemDefaultDevice()!
let commandQueue = device.makeCommandQueue()
let commandBuffer = commandQueue.makeCommandBuffer()
 // Initialize graph
 let graph = MPSNNGraph(device: device, resultImage: makeGraph())
 // Create input image
 let input = MPSImage(texture: texture, ...)
// Encode graph
let output = graph?.encode(to: commandBuffer,
sourceImages: [input])
// Tell GPU to start executing work and wait until GPU work is done
commandBuffer.commit()
commandBuffer.waitUntilCompleted()

```

### // Example: execute graph on the GPU asynchronously

```swift

// Metal setup
let device = MTLCreateSystemDefaultDevice()!
  
// Initialize graph
let graph = MPSNNGraph(device: device, resultImage: makeGraph())
// Create input image
let input = MPSImage(texture: texture, ...)

// Encode graph
let output = graph?.executeAsync(sourceImages: [input]) {
    resultImage, error in
    // check for error and use resultImage inside closure
}

// Don’t wait, encode new GPU task
```

## Demo - Inception-v3 using Neural Network Graph API


