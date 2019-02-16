## [HDR camera and effects](2016-609-3-hdr-camera-and-effects.md) [36:20~41:20]


* HDR is short for High Dynamic Range
* Float components
* Low dynamic range: 8 bits per components
* HDR extends that range
* Tone mapped to LDR screens

* Needed for High Dynamic Range contents
& Can also be used with normal contents but realistic light ranges

```swift
let camera = SCNCamera()
camera.wantsHDR = true
```

### Tone mapping


* Converts from HDR to LDR
* Automatic eye adaptation
* Configurable (gray point, white point, min/max exposure)

```swift
camera.wantsExposureAdaptation = true
camera.averageGray = 0.5
camera.whitePoint = 0.5
camera.exposureOffset = 2.5
camera.minimumExposure = -20.0
camera.maximumExposure = 10.0
```

### Default exposure vs Under exposure vs Over exposure

## Effects

### Bloom

* High-intensity lights and reflections bleeding on the surrounding pixels
* Simulates the effect of being blinded by looking at a bright light


```swift
camera.bloomThreshold = 0.5
camera.bloomIntensity = 1.5
camera.bloomBlurRadius = 2.5
```

### motion blur

* Smoothens camera movements
* Some objects can be excluded from the motion blur

```swift
camera.motionBlurIntensity = 0.2
```

Use movability hint to exclude nodes from the motion blur

```swift
character.movabilityHint = .movable
```

### vignetting

Simulates the round shading aberrations of real camera lenses

```swift
camera.vignettingPower = 0.2
camera.vignettingIntensity = 1.2
```

### Color fringe

Simulates the chromatic aberrations happening in real lenses

```swift
camera.colorFringeStrength = 0.2
camera.colorFringeIntensity = 0.8
```

### Color correction

* Saturation
  * Easy black and white look
  * Overblown colors
* Contrast
  * More intense look

```swift
camera.saturation = 0.0
camera.contrast = 2.0
```


### Color grading

Changes the mood of the rendering by applying a color profile
* 3D color cube
* Lookup table
* Stored as a strip of square images:

```swift
camera.colorGrading = "colorProfile.png"
```

### Summary
Brand new HDR cameras and effects
* Configurable tone mapping and exposure
* Bloom
* Motion blur
* Vignetting
* Color fringe
* Saturation and contrast
* Color grading
