
## Saving and Loading Maps|555|p20



World Tracking
Recap

- Position and orientation
- Physical scale
- 3D feature points
- Relocalization


[`ARWorldMap`](https://developer.apple.com/documentation/arkit/arworldmap)


- Mapping of physical 3D space
- Mutable list of named anchors
- Raw feature points and extent
- Serialization

### Multi-User Experiences


```swift 
// Saving and Loading World Maps
// Retrieve world map from session object
session.getCurrentWorldMap { worldMap, error in
    guard let worldMap = worldMap else {
    showAlert(error)
    return
    }
}

 
// Load world map and run the configuration
let configuration = ARWorldTrackingConfiguration()
configuration.initialWorldMap = worldMap
session.run(configuration)

```

## Acquiring Good World Maps

- Important for relocalization
- Multiple points of view
- Static, well-textured environment
- Dense feature points on the map
 
```swift
open class ARFrame : NSObject, NSCopying {
   open var worldMappingStatus: ARFrame.WorldMappingStatus
}
```

### Using WorldMappingStatus
 
```swift
public enum WorldMappingStatus : Int {
    case notAvailable
    case limited
    case extending
    case mapped 
}
```

•Demo
• Saving and Loading Map


[`ARWorldMap`](https://developer.apple.com/documentation/arkit/arworldmap)


World Tracking Enhancements

- Saving and loading maps
- Faster initialization and plane detection Robust tracking and plane detection More accurate extent and - boundary Continuous autofocus
- New 4:3 video formats


