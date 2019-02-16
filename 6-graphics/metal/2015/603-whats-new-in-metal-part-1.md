
# [603 What's New in Metal, Part 1](https://developer.apple.com/videos/play/wwdc2015/603/)

36:39

Metal in Review
New Feature
Metal and App Thinning


Introducing MetalKit
Metal Performance Shaders

Metal System Trace Tool
Metal Best Practices


Broad Support for Metal [836]

- macOS

### Foundary



## New Features 1528


Metal Feature Set Definitions
Feature sets represent a collection of capabilities by GPU generation

iOS_GPUFamily2_v1


## Shader Constant Updates


Bind per draw

```swift
id <MTLBuffer> constant_buffer = ...;
MyConstants* constant_ptr = constant_buffer.contents;
for (i=0; i<draw_count; i++)
{
    constant_ptr[i] = // write constants directly into the buffer
    [render_pass setVertexBuffer:constant_buffer offset: 0 atIndex : 0];

    :i*sizeof(MyConstants) atIndex:0];
// draw
}
```


### New Memory Model

Support both unified and Discrete Memory model with minimal code change

New storage modes to specify where the resource should reside

- Shared storage mode
- Private storage mode
- Managed storage mode


#### Shared Storage Mode

Introduced with iOS 8

Full coherency between CPU and GPU at command buffer boundaries


#### Private Storage Mode

New with iOS 9 and OS X

Resources are only accessible to GPU—blit, render, compute
Metal can store data more optimally for the GPU

#### Managed Storage Mode

New with OS X

Metal manages where the resource resides

Performance of private memory with convenience of shared


Metal Managed Memory Model

Default storage modes

- Buffers are shared
- Default texture storage mode depends on platform
  - iOS default is shared
  - OS X default is managed


#### Layered Rendering

Rasterize to multiple layers of a texture

Slices of a 2D array texture Plane of a 3D texture

Face of a cube texture

Output the target layer from a vertex shader

struct VSOut {
      float4 position [[position]];
      ushort layer [[render_target_array_index]];
}


#### New Texture Features

Texture usage

New property in the texture descriptor to declare how a texture will be used
Allows the Metal implementation to optimize for that usage

-    MTLTextureUsageUnknown
-    MTLTextureUsageShaderRead
-    MTLTextureUsageShaderWrite
-    MTLTextureUsageRenderTarget
-    MTLTextureUsageBlit


## Metal and App Thinning 2920
