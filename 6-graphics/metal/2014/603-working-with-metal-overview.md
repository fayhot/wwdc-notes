# [Working with Metal: Overview](https://developer.apple.com/videos/play/wwdc2014/603/)

* Background
* API
* Shading language
* Developer tools


## Before Metal

## Metal Design

* Thinnest possible API
* Modern GPU features
* Do expensive tasks less often
* Predictable performance
* Explicit command submission
* Optimized for CPU behavior


### How do we do this?

Frame Times

30 FPS (33.3 milliseconds/frame)

GPU utilization = 67%

CPU time = App + GPU

### Why Is GPU Programming Expensive ?

* State validation
  * Confirming API usage is valid
  * Encoding API state to hardware state
* Shader compilation
  * Run-time generation of shader machine code
  * Interactions between state and shaders
* Sending work to GPU
  * Managing resource residency
  * Batching commands

### Do Expensive Task Less Often

When|Frequency |Before Metal | After Metal
--|--|--|--
Application build | "Never"| | Shader compilation
Content loading| Rare| |  State validation
Draw time | 1000s of times per frame | All | Start work on GPU


## API

### Metal Objects

* Device
* Queue
* Buffer
* Encoder
* State
* Code
* Resources



### Command Submission Model

### Resource Update Model

Two types of resources

* Textures ()
* Buffer

Texture - implementation private storage , metal provide .


Can share texture storage with other textures

* interpret as different pixel formats with same pixel size
* e.g. sRGB vs RGB, or single 32-bit


## Render Command Encoder


## Shading Language 33~

Based on C++11

Additions
* GPU hardware features (texture )

Data types for graphics

"Attributes"
* Function arguments
* Sampling

#### Argument Tables

code to table , in diagram


## Developer tools 36~
