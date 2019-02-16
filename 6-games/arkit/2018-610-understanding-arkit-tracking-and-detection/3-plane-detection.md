## [Plane Detection](3-plane-detection.md) | 2415 | p89

Behind the Scenes

 ```swift
// Create a world tracking configuration
let configuration = ARWorldTrackingConfiguration()
// Enable plane detection
configuration.planeDetection = [.horizontal, .vertical]
// Run the session
session.run(configuration)
```

### Plane Detection API

```swift
open class ARPlaneAnchor : ARAnchor {
    open var transform: simd_float4x4 { get }
    open var center: simd_float3 { get }
    open var extent: simd_float3 { get }
    open var geometry: ARPlaneGeometry { get }
    ... 
}
```