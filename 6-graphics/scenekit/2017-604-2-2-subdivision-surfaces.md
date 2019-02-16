


## [Subdivision Surfaces](2017-604-2-2-subdivision-surfaces.md)  | 2615 | p94 


### Iterative refinement

Edge and vertex sharpness


- Easier and faster to create by artists
- Reduced file sizes and faster load times
- Dynamic control on quality of rendered geometry
- Original support for CPU-based subdivision
- Better support for per-face data interpolation (e.g. texture coordinates)

```swift
// Enable subdivision surfaces
geometry.subdivisionLevel = 1
```

### OpenSubdiv on Metal


- Leverages tessellation with Metal-based GPU backend
- Both uniform and feature-adaptive subdivision are now supported
- Efficient implementation for animated models with skinning and morphing


### Coarse- Refined mesh 

Creases  / 褶痕

### Feature-adaptive and uniform subdivision


```swift
//Subdivision Surfaces
//Adaptive subdivision on the GPU

// Enable subdivision surfaces
geometry. subdivisionLevel = 1
geometry.wantsAdaptiveSubdivision = true

// Enable tessellation
let tessellator = SCNGeometryTessellator()
geometry.tessellator = tessellator
```

<!-- ### Subdivision Surfaces -->

### Faster skinning and morphing | 3000 | p117

- Only the coarse mesh is animated
- Leverages the GPU for morphing, skinning and refinement


```swift
//Subdivision Surfaces
//Asset authoring
// Preserve topology when importing from files
let scene = try! SCNScene(url: url, options: [.preserveOriginalTopology: true])

// Use quads when creating geometries programmatically

let element = SCNGeometryElement(data: elementData,
  primitiveType: .polygon,
  primitiveCount: 1,
  bytesPerIndex: MemoryLayout<UInt8>.size)

```


### Demo - Pottry  | 3100 | p119

Use normal map to add details.

edit geometry


### Tessellation and Subdivision Surfaces | 3340

OS|Configuration
---|---
macOS|All configurations
iOS|A9 chip (iPhone 6s)

