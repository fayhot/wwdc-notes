
#### Layered Rendering

Rasterize to multiple layers of a texture

Slices of a 2D array texture Plane of a 3D texture

Face of a cube texture

Output the target layer from a vertex shader

struct VSOut {
      float4 position [[position]];
      ushort layer [[render_target_array_index]];
}


### Texture Barriers

- GPUs overlap execution of many draw calls
- Output of one draw cannot be safely read by a later draw
- New API to insert barriers between draw calls

### New Texture Features

Texture usage

New property in the texture descriptor to declare how a texture will be used
Allows the Metal implementation to optimize for that usage

- MTLTextureUsageUnknown
- MTLTextureUsageShaderRead
- MTLTextureUsageShaderWrite
- MTLTextureUsageRenderTarget
- MTLTextureUsageBlit



#### Depth/stencil textures

Mac GPUs only support combined depth and stencil formats

constant|note
---|---
Depth32Float_stencil8|Supported on all Metal Devices
Depth24Unorm_stencil8|If available and meets your precision requirements

