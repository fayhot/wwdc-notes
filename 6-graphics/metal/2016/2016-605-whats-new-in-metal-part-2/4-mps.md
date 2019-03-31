
## [Additions to Metal Performance Shaders](4-mps.md)|Anna Tikhonova|3730|p167


Recap
A framework of data-parallel algorithms for the GPU Optimized for iOS
Designed to integrate easily into your Metal applications As simple as calling a library function


Supported image operations

- Convolution: General, Gaussian Blur, Box, Tent, and Sobel Morphology: Min, Max, Dilate, and Erode
- Lanczos Resampling
- Histogram, Equalization, and Specification
- Median Filter
- Thresholding
- Image Integral



New operations

- Wide Color Conversion
- Gaussian Pyramid
- Convolutional Neural Networks (CNNs)


### Some Applications of Deep Learning

X|apps
---|---
Images|Object detection and recognition, image classification and segmentation
Audio|Speech recognition and translation 
Haptics|Sense of touch


Training
Second phase


Convolutional Neural Networks (CNNs)
Biologically-inspired, resemble the visual cortex
Organized into layers of neurons
Trained to recognize increasingly complex features
- First layers trained to recognize low-level features
- Subsequent layers trained to recognize higher-level features
- Last layers combine all generated information to produce output

Building Blocks 

Data

- MPSImage and MPSTemporaryImage

Layers


- Convolution
- Pooling
- Fully-Connected
- Neuron
- SoftMax
- Normalization


### Demo - Detecting a smile


## Convolution Layer



###
