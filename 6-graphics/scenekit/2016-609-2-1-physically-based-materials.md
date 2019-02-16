
### [Physically based Materials](2016-609-2-1-physically-based-materials.md) [13:40~19:55]


Diffuse reflection

Specular reflection

#### Comparison : Plastic vs Aluminum vs Gold

dielectric 绝缘体 has low reflectivity value


Metalness

x | Metal | Dielectric 绝缘体
--|--|--
reflectance|high|low
light | absorb light | absorb and scatter light
specular reflection|bright specular reflection | specular reflection at grazing angles
diffuse reflection|no|mainly
reflectance at 0 degree |__diffuse__ map |constant
x |-|object albedo __diffuse__ map



abdor

specular reflection

#### roughness [17:17]

#### SCNMaterial API

Three fundamental properties

* Albedo or reflectance at 0°
* Metalness
* Roughness

```swift
public class SCNMaterial {
   public var diffuse: SCNMaterialProperty { get }
   public var metalness: SCNMaterialProperty { get }
   public var roughness: SCNMaterialProperty { get }
}
```
New physically based lighting model

diffuse , metalness , and roughness maps

```swift
let material = SCNMaterial()
material.lightingModelName = .physicallyBased
material.diffuse.contents = "albedo.png"
material.metalness.contents = "metalness.png"
material.roughness.contents = "roughness.png"
```
#### Image Examples

diffuse , metalness, roughness

#### Material API

* Use grayscale images for metalness , roughness , and ambientOcclusion
* Use scalars for constant values

```swift
material.metalness.contents = "metalness.png"
material.roughness.contents = NSNumber(value: 0.5)
```
