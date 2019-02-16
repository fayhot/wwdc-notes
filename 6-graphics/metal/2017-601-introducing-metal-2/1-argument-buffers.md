
## [Argument Buffers](1-argument-buffers.md) | 520

### Material Example

property|in Metal as
---|---
roughness|MTLBuffer
intensity|MTLBuffer
surfaceTexture|
specularTexture
sampler|

### Traditional and New


### Reduced CPU Overhead （iPhone 7)


### Benefits

- Improve performance
- Enable new use cases
- Easy to use

### Shader example  


```
struct Material {
  float roughness;
  float intensity;
  texture2d<float>  surfaceTexture;
  texture2d<float>  specularTexture;
  sampler textureSampler;
};

kernel void my_kernel(constant Material &material [[buffer(0)]]) {
  ...
}

```

## New Use Cases 

### Dynamic Indexing - Crowd rendering | 1045

```
vertex VertexOutput instancedShader(
           uint         id    [[instance_id]],
  constant Character *  crowd [[buffer(0)]])
{
  // Dynamically pick the character for given instance index
  constant Character &obj = crowd[id];
  return transformCharacter(obj);
}
```

### Set Resources on GPU - Particle simulation | 1350



```
struct Data {
  texture2d<float> tex;
  float value;
};

kernel void copy(
  constant Data &src [[buffer(0)]],
  device   Data &dst [[buffer(1)]])
{
  dst.value = 1.0f;   //< Assign constants
  dst.tex = src.tex;  //< Copy just a texture
  dst = src;          //< Copy entire structure

}

```

### Multiple Indirections | 1450


- Argument Buffers can reference other Argument Buffers
- Create and reuse complex object hierarchies


```
struct Object {
  float4 position; 
  device Material *material; ///< Many objects can point to the same material
};


struct Tree {
  device Tree *children[2];
  device Object *objects; ///< Array of objects in the node
};
```

#### Support Tiers

x|Tier 1 | Tier 2
---|---|---
x


### Demo | 1640




### API Highlights | 2030

- Argument Buffers are stored in plain MTLBuffer
- Use MTLArgumentEncoder to fill Indirect Argument Buffers
- Abstracts platform differences behind simple interface
- Up to eight Argument Buffers per stage



```
// Shader syntax
struct Particle {
  texture2d<float> surface;
  float4 position;
};

kernel void simulate(constant Particle &particle [[buffer(0)]]) { ... }

// Create encoder for first indirect argument buffer in Metal function 'simulate'
let simulateFunction = library.makeFunction(name:"simulate")!
let particleEncoder = simulateFunction.makeArgumentEncoder(bufferIndex: 0)

// API calls to fill the indirect argument buffer
particleEncoder.setTexture(mySurfaceTexture, at: 0)
particleEncoder.constantData(at: 1).storeBytes(of: myPosition, as: float4.self)

```

### Managing Resource Usage

- Tell Metal what resources you plan to use
- Use Metal Heaps for best performance

```
// Use for textures with sample access or buffers
commandEncoder.use(myTextureHeap)
// Used for all render targets, views or read/write access to texture
commandEncoder.use(myRenderTarget, usage: .write)
```



### Best Practices
Organize based on usage pattern
Per-view vs. per-object vs. per-material Dynamically changing vs. Static
Favor data locality
Use traditional model where appropriate

