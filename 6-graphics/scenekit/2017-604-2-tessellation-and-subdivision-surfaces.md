## [Tessellation and Subdivision Surfaces](2017-604-2-tessellation-and-subdivision-surfaces.md) | Amaury Balliet|  1855 | p52


- How tessellation works
- New Tessellation-based geometry APIs
- Subdivision Surfaces


### Motivation

* Asset comes as a low-resolution model (coarse mesh)
* Decreased memory bandwidth
* High resolution model generated from the coarser model
  * High resolution model not stored in memory
  * Generated on-the-fly by the GPU
  * Control over the amount of detail generated

### Tessellation factors

### SCNGeometryTessellator

```swift
let tessellator = SCNGeometryTessellator() 
geometry.tessellator = tessellator
```

#### Uniform tessellation

```swift
// Uniform tessellation
tessellator.edgeTessellationFactor = 3.0 
tessellator.insideTessellationFactor = 3.0

// Local space tessellation
tessellator.isAdaptive = true 
tessellator.maximumEdgeLength = 0.01 // in local space

// Screen space tessellation
tessellator.isAdaptive = true 
tessellator.isScreenSpace = true 
tessellator.maximumEdgeLength = 50 // pixels
```


## New Tessellation-based geometry APIs | p78

### Shader Modifiers

- Fully supported in tessellation pipeline
- Allow for completely custom effects

```swift
// Shader modifier for the "geometry" entry point
float3 p = _geometry.position.xyz;
float disp = sin(p.x + 5.0 * scn_frame.time) * cos(p.y + 2.5 * scn_frame.time); _geometry.position.xyz += _geometry.normal * disp;
```


### Geometry Smoothing

```swift
// Geometry smoothing
tessellator.smoothingMode = .pnTriangles
```


### Displacement Mapping and

Height Map

```swift
// Height map
material.displacement.contents =  "volcano-height-map.png"
material.displacement.textureComponents = .red
```

Vector Displacement maps


```swift
// Vector displacement map
material.displacement.contents =  "water-drop-displacement-map.exr"
material.displacement.textureComponents = .all
```
