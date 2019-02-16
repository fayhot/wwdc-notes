## [Object Detection](6-object-detection.md)] | 4835 | p204

- Scanning 
- Detection

### Object Scanning

Share ARReferenceObject


### Good Objects to Track

- Rigid objects
- Texture rich
- No Reflective
- No Transparent

## Detection

Object Detection API

```swift
// Load Objects from Assets
let objects = ARReferenceObjects.referenceObjects(inGroupNamed: "Object", bundle: Bundle.main)
guard let objects = objects else { 
    print("Error loading objects")
    return
}

// Create a session configuration
let configuration = ARWorldTrackingConfiguration()
configuration.detectionObjects = objects

// Run the session
let session = ARSession()
session.run(configuration)
```

### Get Results

```swift
func session(_ session: ARSession, didUpdate anchors: [ARAnchor]) {  
    for anchor in anchors {  
        if let objectAnchor = anchor as? ARObjectAnchor {  
            let objectName = objectAnchor.referenceObject.name ?? ""  
            print("Object found: \(objectName)")  
        }  
    }  
} 
```

### Object Detection vs. World Map Relocalization

- Object Detection
- World Map Relocalization
