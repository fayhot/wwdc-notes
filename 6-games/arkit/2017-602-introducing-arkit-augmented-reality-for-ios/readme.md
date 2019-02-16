
# [2017 602 Introducing ARKit: Augmented Reality for iOS](https://developer.apple.com/videos/play/wwdc2017/602/)


## ARKit

Mobile AR platform / High-level API / iOS (A9 and up)

## Features/Levels

### Tracking

* world tracking / visual inertial odometry / no external setup

### Scene Understanding

* Plane Detection
* Hit-Testing
* Light estimate

### Rendering

Easy integration / AR views / custom rendering

## Arch

ARSession

[`ARConfiguration`](https://developer.apple.com/documentation/arkit/arconfiguration)


[`ARFrame`](https://developer.apple.com/documentation/arkit/arframe)

Captured image / tracking information / scene information


## Demo

## Scene Understanding

Stefan Misslinger


### [ARPlaneAnchor]()

Plane Detection

* Horizontal with respect to gravity / Runs over multiple frames / Aligned extent for surface / Plane merging

### Hit-Testing

Intersect ray with real world / uses scene information / Results sorted by distance / hit-test types

#### hit-test types

[`ARHitTestResult.ResultType`](https://developer.apple.com/documentation/arkit/arhittestresult.resulttype)



```swift

let p = CGPoint(x: 0.5, y: 0.5)
let results = frame.hitTest(point, types: [])
if let closestResult = results.first {
  let an
}


```

## Demo 2


## Rendering



### Custom Rendering

Draw camera background / Update virtual camera / update light /
