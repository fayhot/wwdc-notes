
## [New Features](2-new-features.md) | 1528


### Metal Feature Set Definitions

Feature sets represent a collection of capabilities by GPU generation


Feature sets represent a collection of capabilities by GPU generation
Prefix defines the platform
Family Name is unique to a hardware generation
Revision number can change as features are added over time


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

- Introduced with iOS 8
- Full coherency between CPU and GPU at command buffer boundaries


#### Private Storage Mode

- New with iOS 9 and OS X
- Resources are only accessible to GPU—blit, render, compute
- Metal can store data more optimally for the GPU

#### Managed Storage Mode

- New with OS X
- Metal manages where the resource resides
- Performance of private memory with convenience of shared




CPU read back

App must synchronize resource before CPU read

```objc
    [blitCmdEncoder synchronizeResource:myBuffer];
    [cmdBuffer waitUntilCompleted]; // Or use completion handler
    contents = [myBuffer contents];
    [blitCmdEncoder synchronizeResource:myTexture];
    [cmdBuffer waitUntilCompleted]; // Or use completion handler
    [myTexture getBytes:...];
```

Metal Managed Memory Model

Default storage modes

- Buffers are shared
- Default texture storage mode depends on platform
  - iOS default is shared
  - OS X default is managed


2-2-macos-only.md
