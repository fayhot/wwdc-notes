
## [Camera (Effect)](2017-604-1-camera-enhancements.md)

### Demo - [Fox 2](https://developer.apple.com/sample-code/wwdc/2017/Fox2.zip)

[`SCNCamera`](https://developer.apple.com/documentation/scenekit/scncamera)

follow character smoothly.

```swift

//Physically Based Camera

// configure field of view...
camera.fieldOfView = 60.0 //degrees

// ...or focal
camera.focalLength = 50.0  //mm
camera.sensorHeight = 24.0 //mm

```

configure the depth of field

```swift
camera.wantsDepthOfField = true
camera.focusDistance = 0.8 //meters
camera.fStop = 5.6
```

#### Bokeh

Automatic bokeh / Works best with HDR camera

```swift
// configure the camera for HDR
camera.wantsHDR = true

// configure the depth of field
camera.apertureBladeCount = 5
```

#### Motion Blur
```swift
// Activate Motion Blur
camera.motionBlurIntensity = 1.0
```

#### Object Motion Blur

###  Ambient Occlusion [8]

Principle

```swift
// Activate SSAO
 camera.screenSpaceAmbientOcclusionIntensity = 1.0

// Configure SSAO
camera.screenSpaceAmbientOcclusionRadius = 5 //scene units
camera.screenSpaceAmbientOcclusionBias = 0.03 //scene units
camera.screenSpaceAmbientOcclusionDepthThreshold = 0.2 //scene units
camera.screenSpaceAmbientOcclusionNormalThreshold = 0.3
```

### Demo 1 - Anatole Duprat [9]

* camera 1
  * focus distance , smaller - key is near camera.
  * fstop , small number - strong blur
  * illuminance of particle.
* camera 2 - far focus
  * .
* camera 3
  * adjust fstop and focus

### Demo 2 - Motion Blur [10:30]

### Demo 3 - SSAO  

* intensity :
* radius :


## Camera Control - Thomas Goossens [12:40]
