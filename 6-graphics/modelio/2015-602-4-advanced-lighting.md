
## [Advanced Lighting and Baking](2015-602-4-advanced-lighting.md) Remi Palandri [31~41:30]



Advanced Lighting
Global illumination

* Global illumination looks great
* But very expensive
* We want to approximate GI
* Balance performance/quality



### Advanced Lighting - Ambient occlusion

* Measure of geometry occlusion
* Uses offline raytracing
* Input—a mesh and a set of occlusion meshes
* Output—a set of occlusion values
* Stored in vertices or a texture


### Advanced Lighting - MDLMesh operations

```swift
// Bake the spaceship with itself
[shipMesh generateAmbientOcclusionVertexColorsWithQuality:0.6
        attenuationFactor:0.8
        objectsToConsider:@[shipMesh]
        vertexAttributeNamed:@“aoTextureCoord” ];
// Bake the ground floor with its surrounding objects
[groundMesh generateAmbientOcclusionTextureWithQuality:0.6

          attenuationFactor:0.8
          objectsToConsider:@[boxMesh, groundMesh]
          vertexAttributeNamed:@“aoTextureCoord”
          materialPropertyNamed:@“aoTextureProperty” ];
```  

### Demo - Xcode Integration

### Advanced Lighting - Light maps

* Computes the effect of lights
* Supports lots of lights
* Calculated offline
* Complex lights supported
