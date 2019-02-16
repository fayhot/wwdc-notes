
## [Model IO](607-1-metalkit-modelio.md) || 1300

Rendering a Model I/O Asset

- Metal Render State Pipeline
- Model I/O Asset Initialization
- MetalKit Mesh and Submesh Objects
- Metal Render State Setup and Drawing


### Step 1: Metal Render State Pipeline

Vertex Shader

Setting up Per-Vertex Inputs

```

struct VertexInput {
    float3  position [[ attribute(0) ]];
    float4  color    [[ attribute(1) ]];
    float2  texUV    [[ attribute(2) ]];
};
vertex VertexOutput vertexFunction(
  VertexInput current [[ stage_in ]])
{
...
}
```

Vertex Descriptor

```
MTLVertexDescriptor *metalVertexDesc = [MTLVertexDescriptor new];

metalVertexDesc.attributes[0].format = MTLVertexFormatFloat3;
metalVertexDesc.attributes[0].offset = 0;

metalVertexDesc.attributes[1].format = MTLVertexFormatUChar4Normalized;
metalVertexDesc.attributes[1].offset = 12;

metalVertexDesc.attributes[2].format = MTLVertexFormatHalfFloat2;
metalVertexDesc.attributes[2].offset = 16;

metalVertexDesc.layouts[0].stride = 20;

```

### Building the Pipeline
```
renderPipelineDescriptor.vertexDescriptor = metalVertexDesc;
MTLRenderStatePipeline *pipeline =
[device.newRenderPipelineStateWithDescriptor:renderPipelineDescriptor error:error];
```


### Setup for Model Rendering

Asset initialization

Asset Initialization

#### Model I/O Vertex Descriptor vs. Metal Vertex Descriptor

- Model I/O Vertex Descriptor
  - Describes the layout of vertex attributes in a mesh
- Metal Vertex Descriptor
  - Describes the layout of vertex attribute inputs to a render state pipeline

Intentionally designed to look similar

Both contain an array of attribute and buffer layout objects Simplifies translation from one type to other

### MetalKit Mesh Buffer Allocator

```
MTKMeshBufferAllocator *mtkBufferAllocator =
    [[MTKMeshBufferAllocator alloc] initWithDevice:metalDevice];
```

```
NSArray<MTKMesh *> *meshes = [MTKMesh meshesFromAsset:asset device:device];
```

### Step 4: Mesh Rendering with Metal -  Setup for model rendering

```
NSUInteger bufferIndex = 0;
for(MTKMeshBuffer *vertexBuffer in mesh.vertexBuffers) {
    if(vertexBuffer.buffer != nil) {
        [renderEncoder setVertexBuffer:vertexBuffer.buffer
        offset:vertexBuffer.offset
        atIndex:bufferIndex];
    }
    bufferIndex++;
}
```
