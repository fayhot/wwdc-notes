
## [World Tracking](2-world-tracking.md) | 722 | p25


Behind the Scenes—Inertial Odometry
Motion sensor

Behind the Scenes—Visual Odometry
Computer vision

Behind the Scenes—Visual Inertial Odometry
Motion data and computer vision

Behind the Scenes—Visual Inertial Odometry
Initialization


Behind the Scenes
Augmentation


 Behind the Scenes—Visual Inertial Odometry
Tracking


 Behind the Scenes—Visual Inertial Odometry
Optimization for robust tracking


```swift 
ARWorldTrackingConfiguration
open class ARCamera : NSObject, NSCopying {
    open var transform: simd_float4x4 { get }
    open var trackingState: ARTrackingState { get }
    open var trackingStateReason: ARTrackingStateReason { get }
    ... 
}
```

World Tracking Quality

- Uninterrupted sensor data
- Textured environments
- Static scenes


World Tracking Quality—Behind the Scenes

“Health Monitoring”

Tracking State

 
// Called when tracking state changed
func session(_ session: ARSession, cameraDidChangeTrackingState camera: ARCamera) {
    if case .limited(let reason) = camera.trackingState { // Guide user to improve tracking state
        ...
    } 
}

World Tracking
Take-aways

- Tracks orientation and position (6 DoF)
- Augmentation into your physical world
- World Map
- Guide user to achieve best tracking quality
- Runs on your device only
- “Building Your First AR Experience”
