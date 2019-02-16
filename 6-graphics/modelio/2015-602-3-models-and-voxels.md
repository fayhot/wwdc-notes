## Models and Voxels - Claudia Roberts [23:15~31]

Agenda

* Geometry and modeling in Model I/O
* Normal smoothing Subdivision surfaces
* Voxels
* Demo


### Normal Smoothing - Shared vertex normals

* Approximates curvature of more complicated geometry
* Flat vs smooth shading
* Add smoothed out normals to the spaceship

```swift
[spaceship addNormalsWithAttributeNamed:@“normals” creaseThreshold:0.5];
```

### Subdivision Surfaces - Vary surface detail

* Generate subdivided mesh from source mesh
* Increase level of detail only when and where necessary

```swift
MDLMesh *mesh = [MDLMesh newSubdividedMesh:spaceship   submeshIndex:0
                         subdivisionLevels:2];
```

### Voxels - Physical realism

* Volumetric representation consistent with the real world
* Procedural modeling/generation
* Easily explore dataset via neighborhood, child traversal
* Facilitates real-world operations like slicing and cutting
* Constructive Solid Geometry operations


### Voxels - MDLVoxelArray

* Sparse volume grid accessed by a spatial index Quick neighbor finding
* Interior, exterior, surface shell levels
* Model healing and clean-up
* Create polygonal mesh from voxels


### Voxels - MDLVoxelArray operations

```swift
// Set voxels corresponding to mesh
[grid setVoxelsForMesh:m divisions:25 interiorShells:0.f exteriorShells:0.f];
// Given a second MDLVoxelArray, perform boolean operations
[grid intersectWithVoxels:voxels];
[grid unionWithVoxels:voxels];
[grid differenceWithVoxels:voxels];
// Retrieve voxel data
NSData *voxelData = [grid getVoxelIndices];
// Create mesh from voxel grid
MDLMesh *mesh = [grid meshUsingAllocator:allocator];
```

### Demo - Voxels
