
## Camera Control - Thomas Goossens [12:40] | p30

### Common challenges

- Object inspection and scene browsing
- Camera with a behavior


### Object inspection and scene browsing

Previously
* Directly manipulate the camera position, rotation or transform
* For debugging use allowsCameraControl API

New in iOS 11

* Introducing SCNCameraController
* Built-in support for common controls modes
* Default camera controller provided by SCNView



```swift
// turn on camera control
scnView.allowsCameraControl = true
// configure the camera control behaviour
scnView.defaultCameraController.interactionMode = .orbitTurntable
scnView.defaultCameraController.inertiaEnabled = true
scnView.defaultCameraController.maximumVerticalAngle = 45 //degrees
```

name|Description
---|---
Orbit Turntable|Orbit your camera around a 3D, and will provent roll - horizon will always remain level, regardless 
Orbit Arcball|orbit the camera using the vertical and horizontal axes in screen space.  doesn't prevent roll
Orbit Angle Mapping
Fly| more suitable for  lap scenes you want to navigate into. center of rotation of the camera is camera itself, you rotate the camera to look around in a position to orbit around an object.
Pan|
Roll|
Frame nodes|
Dolly|
Inertia|
Truck|



orbitTurntable

orbit Arcball







[`SCNCameraController`](SCNCameraController)

[`SCNCameraControllerDelegate`](https://developer.apple.com/documentation/scenekit/scncameracontrollerdelegate)


[`SCNCameraControlConfiguration`](https://developer.apple.com/documentation/scenekit/scncameracontrolconfiguration)

### Camera with a behavior | 1535

Chain SCNConstraint objects to define a camera behavior

#### 4 old

SCNLookAtConstraint / SCNTransformConstraint / SCNBillboardConstraint / SCNIKConstraint

#### 5 new

constraint | description
--|--
SCNDistanceConstraint|forces a node to keep a minimum and maximum distance with another specified target node.
SCNReplicatorConstraint|replicate a node position and orientation with an optional offset
SCNAccelerationConstraint|ensure that the node won't move or accelerate faster than a given maximum velocity and acceleration.
SCNSliderConstraint
SCNAvoidOccluderConstraint


### Building a behavior from constraints


SCNReplicatorConstraint - SCNLookAtConstraint - SCNAccelerationConstraint

## Constraints

[API](https://developer.apple.com/documentation/scenekit/constraints)


### Node manipulation helpers | p51

- Math helpers on SCNNode for common transformations
- Vector conversion from node to node
- SCNNode transforms properties available as SIMD types

```swift
// Working with SIMD
aNode.simdPosition += aNode.simdTransform * anotherNode.simdPosition
```

simd limitation:

* not KVC, KVO compliant
* not be included as an NSValue.
