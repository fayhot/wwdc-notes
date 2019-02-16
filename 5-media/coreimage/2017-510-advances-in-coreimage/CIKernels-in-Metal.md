## [CIKernels-in-Metal.md](CIKernels-in-Metal.md) | Tony | 630

### Writing CIKernels

Previously, kernels are written in CIKernel Language
* Based on GLSL
* Language extensions to enable automatic tiling and subregion rendering
  * destCoord()
  * samplerTransform(sampler src, vec2 p)
  * sample(sampler src, vec2 p)
* Translated, concatenated, and compiled at run-time to Metal or GLSL

### Compiling CIKernels on First Render

* Translate CIKernels
* Compile CIKernels to Intermediate Representation
* Concatenate CIKernels
* Compile to GPU Code

### Writing CIKernels in Metal (New) | p39

Now, you can write CIKernels directly in Metal Shading Language

Benefits
* Precompiled at build-time with error diagnostics
* More modern language features
* Still supports concatenation and tiling
* Can be mixed with traditional CIKernels not written in Metal

Supported on iOS (for A8 or newer devices), macOS, and tvOS



Compiling

## How to Create Metal CIKernels | 1100 | p46

### Steps

1. Write CIKernel in Metal shader file
2. Compile and link Metal shader file
3. Initialize CIKernel with function from Metal library


### 1. [Write CIKernel in Metal shader file](2.1-wriing-cikernel-in-metal-shader-file.md)


### 2. Compile and link Metal shader file

File | extension | source/program
--|--|--
CIKernel Source File| .metal |
Intermediate Representation File|.air | metal -fcikernel
Metal Library Data File|.metallib | metalib -cikernel

#### Xcode | 1700

Target - Build Settings - Search Metal

Key | Value
--|--
Other Metal Compiler Flags| -fcikernel
`MTLLINKER_FLAGS`  | -cikernel

#### xcrun

```
xcrun metal -fcikernel MyKernels.metal -o MyKernels.air
xcrun metallib -cikernel MyKernels.air -o MyKernels.metallib
```


### 3. Initialize CIKernel with function from Metal library

#### New [`CIKernel`](https://developer.apple.com/documentation/coreimage/cikernel) API


* [`convenience init(functionName name: String, fromMetalLibraryData data: Data) throws`](https://developer.apple.com/documentation/coreimage/cikernel/2880194-init)
* [`convenience init(functionName name: String, fromMetalLibraryData data: Data, outputPixelFormat format: CIFormat) throws`](https://developer.apple.com/documentation/coreimage/cikernel/2880195-init)

```swift

// Example of initializing CIKernels
let url = Bundle.main.url(forResource: "default", withExtension: "metallib")!
let data = try! Data(contentsOf: url)

let kernel = try? CIKernel(functionName: "myKernel", fromMetalLibraryData: data)
let warpKernel = try? CIWarpKernel(functionName: "myWarp", fromMetalLibraryData: data)
let colorKernel = try? CIColorKernel(functionName: "myColor", fromMetalLibraryData: data)
```
