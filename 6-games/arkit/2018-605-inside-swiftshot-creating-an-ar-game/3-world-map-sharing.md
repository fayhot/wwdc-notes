
## [Sharing a World Map](3-world-map-sharing.md) | | 11? | p41

### Saving

- First device scans area, captures features
- Asks ARSession for world map
- Serializes to disk

```swift
sceneView.session.getCurrentWorldMap { map, error in
    if let error = error { print(error); return }
    guard let map = map, let data = try? NSKeyedArchiver.archivedData (
        withRootObject: map, requiringSecureCoding: true) else { return }
        // save or send over network
    } 
}
```


### Sharing a World Map
Ad-hoc gaming 

- Share over network
  - Peer-to-peer network connection
  - Encrypt data in flight
  - UI guidance to aid relocalization


### Sharing a World Map - Fixed installations


- Prerecord world maps for specific installation areas
- Distribute to managed devices
- Use iBeacons to automatically select correct world map for each location

Sharing a World Map
Loading
NEW
 
```swift 
// Unarchive data to ARWorldMap
let worldMap = try NSKeyedUnarchiver.unarchivedObject(ofClass: ARWorldMap.self, from: data)
// Create tracking configuration
let configuration = ARWorldTrackingConfiguration() configuration.initialWorldMap = worldMap
// Run session
sceneView.session.run(configuration, options: [.resetTracking, .removeExistingAnchors])
```

### Sharing a World Map - Privacy

- ARWorldMap uses features of the world around you
  - No latitude/longitude information
  - May include personally identifiable information
- Treat serialized ARWorldMap as user-private data
  - Encrypt at rest and in motion
  - Obtain user consent for extended usage


Sharing a World Map
ARAnchor

- ARAnchor represents a location and orientation in the physical world
  - ARKit adds anchors for planes, objects, and images
  - Also created and added via API
• •
let anchor = ARAnchor(name: “Touched”, transform: transform) session.add(anchor: anchor)


```swift
// Custom subclass of ARAnchor to annotate game location
class BoardAnchor: ARAnchor {
    private(set) var size: CGSize
    init(name: String, transform: float4x4, size: CGSize) {
        self.size = size
        super.init(name: name, transform: transform)
    }

    required init?(coder aDecoder: NSCoder) {
        self.size = aDecoder.decodeCGSize(forKey: "size")
        super.init(coder: aDecoder)
    }

    override func encode(with aCoder: NSCoder) {
        super.encode(with: aCoder)
        aCoder.encode(size, forKey: "size")
    }

```