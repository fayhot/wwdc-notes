
## [Raster Order Groups](2-raster-order-group.md)  (Richard Schreyer)| 2600|  p92


* Ordered memory access from fragment shaders
* Enables new rendering techniques
  * Order-independent transparency
  * Dual-layer GBuffers
  * Voxelization
  * Custom blending



### Fragment Shaders with Blending

Mid-Shader Memory ..


```
// Blending manually to a pointer in memory
fragment void BlendSomething(
  texture2d<float, access::read_write> framebuffer [[texture(0), raster_order_group(0)]]) {

  float4 newColor = ...
  // Hardware waits on first access to raster ordered memory
  float4 priorColor = framebuffer.read(framebufferPosition);
  float4 blended = custom_blend(newColor, priorColor); 
  framebuffer.write(blended, framebufferPosition);
}
```

### Summary

- Synchronization between overlapping fragment shader threads
- Check for support with MTLDevice.rasterOrderGroupsSupported
