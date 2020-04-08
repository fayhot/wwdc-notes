[2019 604 Introducing ARKit 3](https://developer.apple.com/videos/play/wwdc2019/604)


### People Occlusion



- Enables virtual content to be rendered behind people
- Works for multiple people in the scene
- Works for fully and partially visible people
- Integrated with ARView and ARSCNView
- Depth estimation 
- Available on A12 and later


```swift
class ARConfiguration : NSObject {
    var frameSemantics: ARConfiguration.FrameSemantics { get set }
    class func supportsFrameSemantics(ARConfiguration.FrameSemantics) -> Bool
}
```



### Motion Capture


- Tracks human body in 2D and 3D
- Provides skeleton representation
- Enables driving a virtual character 
- Available on A12 and later


### 2D Body Detection

Result data
ARBody2D provided in ARFrame Contains 2D skeleton



### 3D Motion Capture
Concept

- Tracks a human body pose in 3D space 
- Provides a 3D skeleton representation 
- Provides scale estimation
- Anchored in world coordinates


### ARBodyTrackingConfiguration

- 3D body tracking
- 2D body detection frame semantics enabled by default
- Selected world tracking features available


### Simultaneous Front and Back Camera

- AR experiences using front and back camera
- Enables World Tracking with face data
- Enables Face Tracking with device orientation and position 
- Supported on A12 and later


## Collaborative Session | Thomas Berton, ARKit Engineer | 26:00 | p104





### Saving and Loading Maps (ARKit 2) - Recap

- Enables multi-user experiences
- Ability to save and load ARWorldMap on multiple devices
- One-time map sharing between devices

### Collaborative Session (ARKit 3)

- Continuously shares mapping information between multiple devices Ad-hoc multi-user experiences
- ARAnchors shared and identifiable on all devices
- Individual coordinate systems




Coaching in AR Apps
On-boarding
Throughout the experience
Human interface guideline recommendations



AR Coaching View
Built-in UI overlay for AR applications Guides users to good tracking experience Consistent design throughout applications Automatic activation and deactivation Adjustable coaching goals





Scene Understanding Improvements

- Up to 100 images Automatic scale estimation - Quality feedback at runtime
- ML-enhanced object detection Faster recognition - More robust
- ML-supported plane estimation More accurate boundaries - Faster extension




Raycasting

- Ideal for object placement
- Supports any surface alignment Raycasts tracked over time
- Benefits from plane estimation updates


Visual Coherence Enhancements


- Activated and deactivated automatically based on device capabilities
- Can be explicitly disabled in render options


x


