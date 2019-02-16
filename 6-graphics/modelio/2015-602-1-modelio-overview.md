# Model I/O Overview

## File Formats

## Import and Export

```swift
Import
MDLAsset *asset = [[MDLAsset alloc] initWithURL:myURL]; Export
[asset exportAssetToURL:myURL];
```

## Physical Realism

* Realistic lights
  * IES profile, temperature, image based
* Realistic materials
  * Lambert / Blinn-Phong, physical BRDF
* Realistic cameras
  * From lens to sensor
* Realistic environments
  * Panoramic photographs
  * Procedural skies


## Modify and Bake Assets

```swift
Ambient occlusion
[mesh generateAmbientOcclusionTextureWithQuality: ... ]; Light and shadow baking
[mesh generateLightMapTextureWithQuality: ... ];
Normals calculation
[mesh addNormalsWithAttributeNamed: ... ];
Tangent basis
[mesh addTangentBasisForTextureCoordinateAttributeNamed: ... ];
```
## Voxels

```swift
Create voxels from an asset
[[MDLVoxelArray alloc] initWithAsset: ... ];
Find voxels in a region
NSData *indices = [voxels voxelsWithinExtent:extent];
Constructive solid geometry
[voxels unionWithVoxels:sphereVoxels];
Create a mesh
MDLMesh *mesh = [voxels meshUsingAllocator:allocator];
```

## System Integration

* SceneKit, Metal, and OpenGL
* Preview in Finder and QuickLook
* Edit in Xcode
* Playgrounds and Swift support
