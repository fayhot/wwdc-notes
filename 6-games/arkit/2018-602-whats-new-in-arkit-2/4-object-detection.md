
Object Detection

- Detection of a known static 3D object
- Objects need to be scanned first
- Well-textured, rigid, non-reflective
- Position and orientation
- Integrated into world tracking



// Object Detection
// Create a world tracking configuration
let configuration = ARWorldTrackingConfiguration()
 // Set of objects to be detected
 configuration.detectionObjects = [ancientBust, clayPot]
 



### Object Scanning

- Accumulated scene information
- Transform, extent, center
- Supported by Xcode asset catalog
- ARObjectScanningConfiguration
- Sample code available
  - Scanning and detecting 3D objects


[`ARObjectScanningConfiguration`](https://developer.apple.com/documentation/arkit/arobjectscanningconfiguration)


[`ARReferenceObject`](https://developer.apple.com/documentation/arkit/arreferenceobject)


[`ARObjectAnchor`](https://developer.apple.com/documentation/arkit/arobjectanchor)


