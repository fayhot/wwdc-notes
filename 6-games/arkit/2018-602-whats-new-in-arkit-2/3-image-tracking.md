


Image Detection
Recap

- Recognition of known static 2D images
- Position and orientation
- Integrated into world tracking
- Supported by Xcode asset catalog


Image Tracking

- Images don’t need to be static
- Position and orientation for every frame
- Track multiple images simultaneously
- ARImageTrackingConfiguration

### Using Good Images

- Distinct features Well textured Good contrast


- Repetitive structures Uniform color regions Narrow histogram



### Configurations for Image Tracking


ARWorldTrackingConfiguration
Image anchors in world reference frame
 • •
• •
 Detected images can be tracked ARImageTrackingConfiguration
Independent from world tracking Position and orientation for every frame



```swift
// Image Tracking
// Create an image tracking configuration
let configuration = ARImageTrackingConfiguration()
// Set of images to be tracked
 configuration.trackingImages = [catPhoto, dogPhoto, birdPhoto]
// Optionally specify the maximum number of images to track in parallel
configuration.maximumNumberOfTrackedImages = 2
// Run the session
session.run(configuration)
```