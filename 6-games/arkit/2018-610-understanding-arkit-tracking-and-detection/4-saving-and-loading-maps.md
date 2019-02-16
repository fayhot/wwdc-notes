
## [Saving and Loading Maps](4-saving-and-loading-maps.md) | 3000 | p107

- Acquire a good World Map
- Share the World Map
- Relocalize to World Map


- Internal tracking data
  - Map of 3D feature points
  - Local appearance
- List of named anchors
- Serializable

### Acquiring a Good World Map

- Dense feature points on map
- Static environment
- Multiple points of view
- World mapping status


Acquiring a Good World Map
Guide the user
Indicate mapping status
Warn about limited tracking state Guide relocalization

Share the World Map

```swift
// Retrieve world map from ARSession
session.getCurrentWorldMap { worldMap, error in 
    guard let worldMap = worldMap else {
        showAlert(error)
    return  
    }
    // Serialize
    let data = try NSKeyedArchiver.archivedData(withRootObject: worldMap, requiringSecureCoding: true)
}
```

For shared experiences—MultipeerConnectivity framework  See sample “Creating a Multiuser AR Experience”

Relocalize to World Map
Setup configuration

```swift 
// Receive / Load world map
let worldMap : ARWorldMap = ...
// Create a session configuration
let configuration = ARWorldTrackingConfiguration() configuration.initialWorldMap = worldMap
// Run the session
session.run(configuration)
```

- Setup configuration
- Before Relocalization 
  - Tracking state is Limited with reason Relocalizing
  - World origin is first camera
- After Relocalization
  - Tracking state is Normal  
  - World origin is initial world map
  - Only minor changes in environment allowed