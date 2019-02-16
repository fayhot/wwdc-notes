
# [2014 604 Working with Metal: Fundamentals](https://developer.apple.com/videos/play/wwdc2014/604/)



## Initialization

* Device
* CommandQueue
* Resources (Buffers and Textures)
* RenderPipelineState
* View

### Get the Device


## Drawing

* command buffer
* start a render pass
* draw
* commit the command buffer

### 1 command buffer

let buffer = queue.commandBuffer

### 2 Render Pass Configuration

[`MTLRenderPassDescriptor`](https://developer.apple.com/documentation/metal/mtlrenderpassdescriptor)

get encoder

### 3 Drawing (a Triangle)


### 4 Committing a CommandBuffer

```swift
commandBuffer.addPresent(drawable)
commandBuffer.commit()
```


## Uniform and ...


render.setVertexBuffer(uniformBuffer, offset: 0 at: 1)

### CPU and GPU Pipelining

```swift
dispatch_semaphore_create(3)


{ // Per frame
  wait(, FORVER)

  commandBuffer.addCommandHandler() {
    signal()
  }
}
```


## [Metal shading language](604.2-metal-shading-language.md)

* writing shaders in metal
* data types in metal
* shader inputs, outputs, and matching rules.
