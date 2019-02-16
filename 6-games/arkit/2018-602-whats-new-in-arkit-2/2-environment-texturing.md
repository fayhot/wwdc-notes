## Environment Texturing



### Realistic Rendering

- Position and orientation
- Scale
- Lighting
- Shadow
-  Reflection of textures



### Environment Texturing

- Gathers scene texture
- Cube map representation
- Used as reflection probe
- Reflective objects


AREnvironmentProbeAnchor

- Cube map (MTLTexture)
- Physical extent
- Same lifecycle as other anchors
- Integrated in ARSCNView
- Manual placement

```swift
// Enable manual placement
configuration.environmentTexturing = .manual
```

Demo
• Environment Texturing


