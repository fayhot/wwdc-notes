### [Dolly Zoom](dolly-zoom.md) Stephen Ward, 3625


Metal

Mesh

Vertex shader

Fragment shader

CIImageProcessorKernel


#### Dolly Zoom Effect Vertex Shader

```swift

vertex OutVertex vertexShader(vertices, constants, depthTexture, texSampler, ...) {
  // Sample the vertex’s depth.
  float z = depthTexture.sample(texSampler, vertices[vid].texCoord).r;

  // Compute the scale and new vertex position to achieve the 3D effect
  float zt = constants.threhold   ;
  float dz = constants.strength   ;
  float scale = (z/zt) * ((zt + dz)/(z + dz));
  float2 newPosition = vertices[vid].position. * scale;


  OutVertex vertex;  // Output a transformed vertex
  vertex.position = float4(newPosition, z, 1.0);
  vertex.texCoord = vertices[vid].texCoord;
  return vertex;
}
```

#### Dolly Zoom Effect Fragment Shader


```swift

fragment float4 fragmentShader(
  OutVertex vertex [[stage_in]],
  texture2d<float, access::sample> imageTexture [[texture(0)]],
  sampler texSampler [[sampler(0)]])
{
  return imageTexture.sample(texSampler, vertex.texCoord);
}
``
