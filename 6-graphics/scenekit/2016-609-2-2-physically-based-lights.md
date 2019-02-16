
### [Physically based Lights](2016-609-2-2-physically-based-lights.md) [19:55~25:00]

3 categories

* image based lighting (IBL)
* light probes
* point lights

#### image based lighting

* Cube map captures the environment
* Lighting information is derived from cube map
* Image based lighting can be used alone
* Not mandatory to add lights in the scene


A single change affects the whole scene

```swift
let scene = SCNScene()
scene.lightingEnvironment.contents = "outside.exr"
```

Caveats

* Captures the distant environment
* Does not account for obstacles in the scene
* Not suited for occluded objects

#### Light probes

* A special kind of light
* Captures the local diffuse lighting
* Account for obstacles in the scene
* Lightweight
* Efficient

A special kind of light: SCNLightType.probe


```swift  
let light = SCNLight()
light.type = .probe
```


Can be placed programmatically or in Xcode Static lighting information must be baked

```swift
public class SCNRenderer {
    public func updateProbes(_ probes: [SCNNode], atTime time: CFTimeInterval)
}
```


#### Point lights

Work with physically based materials, too
Updated to be configured with real-world properties

```swift
public let SCNLightTypeOmni: String        // Omnidirectional light
public let SCNLightTypeDirectional: String // Directional light
public let SCNLightTypeSpot: String        // Spot light
```

#### Point lights: Intensity

Expressed in lumens (lm)

```swift
let light = SCNLight()
light.intensity = 1500 // defaults to 1000 lm
```

#### Point lights: Temperature

* Expressed in Kelvin (K)
* Modulates the light’s color

```swift
let light = SCNLight()
light.temperature = 5000
```

temperature

#### Photometric lights

IES light .

* New kind of point light
* Modeled after real-world lights
* Custom attenuation shape


```swift
let light = SCNLight()
light.type = .IES
light.iesProfileURL = Bundle.main().urlForResource("spot", withExtension: "ies")
```
