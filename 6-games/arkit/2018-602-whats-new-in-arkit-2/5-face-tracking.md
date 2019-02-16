

Face Tracking


Recap
Robust face detection and tracking Position and orientation for every frame Fitted triangle mesh/ARFaceGeometry ARFaceAnchor



Directional Light Estimation
Uses face as light probe
Light intensity, direction, color temperature Spherical harmonics coefficients




Gaze tracking  - NEW

```swift
open class ARFaceAnchor : ARTrackable {
    open var leftEyeTransform: simd_float4x4 { get } 
    open var rightEyeTransform: simd_float4x4 { get } 
    open var lookAtPoint: simd_float3 { get }
}
```

Tongue support
NEW

```swift  
extension ARFaceAnchor.BlendShapeLocation {
    public static let tongueOut:
            ARFaceAnchor.BlendShapeLocation
}
```