# [2018 609 Metal for Accelerating Machine Learning](https://developer.apple.com/videos/play/wwdc2018/609/)


609-metal-for-accelerating-machine-learning/readme.md


Anna Tikhonova

GPU-accelerated primitives, optimized for iOS and macOS

- Image processing
- Linear algebra
- Machine learning — inference and training [New]
- Ray tracing [New ]

Training and Inference
Image classification example

Inference
Image classification example


### CNN Inference Enhancements - FP16 accumulation

Available with Apple A11 Bionic GPU for
Convolution Convolution transpose
Sufficient precision for commonly used neural networks Delivers better performance than FP32
NEW

```swift
let conv = MPSCNNConvolutionNode(source: MPSNNImageNode(handle: nil), weights: MyWeights(withFile:“conv.dat”))
conv.accumulatorPrecisionOption = .half
```

## CNN Training

### Network - Handwritten digit recognition


- Convolution
- ReLu
- Max Pooling
- Fully-Connected Dropout
- SoftMax


### Trained Parameters - For inference

Training
Initializing weights

Iterative process

- Forward Pass
- Loss Computation
- Gradient Pass
- Update Weights





## [Training a Neural Network with MPS](2-cnn-training-code.md)

- Create training graph
- Prepare inputs
- Specify weights
- Execute graph
  - Graph updates weights
- Complete training process | | p105

## Demo -  Object detection training using Turi Create with MPS | 2500



## RNN Training


## [RNN Training - code](4-rnn-training-code.md)
