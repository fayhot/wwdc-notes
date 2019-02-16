
## [Image Tracking](5-image-tracking.md) | 3755 | p147

### Behind the Scenes

Localize the image

Dense tracking

### Image Tracking API

- ARReferenceImage
- ARWorldTrackingConfiguration
- ARImageTrackingConfiguration
- ARSession
- ARFrame
- ARImageAnchor

### Adding Images as Assets

- Create AR Resource Group
- Drag images to be detected
- Set physical dimension for images

### Setting Physical Dimension for Images

- Physical image size must be known
- Allows content to be in physical dimension
- Consistent with world tracking data

### Good Images to Track

- High texture
- High local contrast
- Well distributed histogram
- No repetitive structures

### Reference Image Quality in Xcode

- Each image is analyzed
- Similar images
- 


### Reference Image Quality—Tips

Use multiple AR Resource Groups

- Allow many more images to be detected
- Max 25 images per group recommended
- Switch between groups programmatically

### Image Tracking Configurations


Config | ARImageTrackingConfiguration|ARWorldTrackingConfiguration
---|---|---
Feature|Standalone image tracking<br/>No world origin|Image and World tracking<br/>Scene understanding available

```swift 
// Load Images from Assets
let imageSet = ARReferenceImage.referenceImages(inGroupNamed: "Room1", bundle: Bundle.main)
guard let imageSet = imageSet else {
    print("Error loading images")
    return
}

// Create a session configuration
let configuration = ARImageTrackingConfiguration()
configuration.trackingImages = imageSet

// Run the session
let session = ARSession()
session.run(configuration)
```

### Getting Results
 
```swift
func session(_ session: ARSession, didUpdate anchors: [ARAnchor]) {  
    for anchor in anchors { for anchor in anchors {
        if let imageAnchor = anchor as? ARImageAnchor {...}  
    }
}

 
open class ARImageAnchor : ARAnchor, ARTrackable {
  open var transform: simd_float4x4 { get }
  open var referenceImage: ARReferenceImage { get }
  public var isTracked: Bool { get }
}

```

### Absolute Coordinate Space for Shared Experiences



