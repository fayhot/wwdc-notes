# [2017 601 Introducing Metal 2](https://developer.apple.com/videos/play/wwdc2017/601/)


* Michal Valient, GPU Software Engineer
* Richard Schreyer, GPU Software Engineer


## Other Sessions Intro.



## Agenda | 350

Topic(speaker)|time|page
--|--|--
[Argument Buffers](1-argument-buffers.md) | 520
[Raster Order Groups](2-raster-order-group.md)  (Richard Schreyer)| 2600|  p92
[ProMotion Displays](3-promotion-displays.md)| 3150 |p107
[Direct to Display](4-direct-to-display.md) | 3950 | p121
Everything Else | 4550 | p140


## [Argument Buffers](1-argument-buffers.md) | 520

## [Raster Order Groups](2-raster-order-group.md)  (Richard Schreyer)| 2600|  p92

## ProMotion Displays | 3150 | p92

## Direct to Display | 3950 | p121


## Everything Else | 4550 | p140

### Memory Usage Queries

- New APIs to query memory usage per allocation
  - `MTLResource.allocatedSize`
  - `MTLHeap.currentAllocatedSize`
- Query total GPU memory allocated by the device
  - `MTLDevice.currentAllocatedSize`

### SIMDGroup-scoped Data Sharing

Share data across a SIMDGroup

```swift
simd_broadcast(data, simd_lane_id) 
simd_shuffle(data, simd_lane_id) 
simd_shuffle_up(data, simd_lane_id) 
simd_shuffle_down(data, simd_lane_id) 
simd_shuffle_xor(data, simd_lane_id)
```

### Non-Uniform Threadgroup Sizes

### Viewport Arrays

- Vertex Function selects which viewport
- Useful for VR when combined with instancing

### Multisample Pattern Control

- Select where within a pixel the MSAA Sample Patterns are located
- Useful for custom anti-aliasing

### Resource Heaps

- Now available on macOS
- Control time of memory allocation
- Fast reallocation and aliasing of resources
- Group related resources for faster binding

### Other Features

Feature| Summary
---|---
Linear Textures|Create textures from a MTLBuffer without copying
Function Constant for Argument Indexes|Specialize bytecodes to change the binding index for shader arguments
Additional Vertex Array Formats |Add some additional 1 component and 2 component vertex formats, and a BGRA8 vertex format
IOSurface Textures| Create MTLTextures from IOSurfaces on iOS
Dual Source Blending|Additional blending modes with two source parameters


## Summary | 5200
