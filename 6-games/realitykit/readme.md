# Reality (since 2019/iOS13)


WWDC

- [2019 603 Introducing RealityKit and Reality Composer](https://developer.apple.com/videos/play/wwdc2019/603)
- [2019 605 Building Apps with RealityKit](https://developer.apple.com/videos/play/wwdc2019/605)
- [2019 609 Building AR Experiences with Reality Composer](https://developer.apple.com/videos/play/wwdc2019/609)




## Entity and its subclasses

class [`Entity`](https://developer.apple.com/documentation/realitykit/entity)

subclass|x
---|---
class [`AnchorEntity`](https://developer.apple.com/documentation/realitykit/anchorentity)|
class [`ModelEntity`](https://developer.apple.com/documentation/realitykit/modelentity)|
class [`BodyTrackedEntity`](https://developer.apple.com/documentation/realitykit/bodytrackedentity) |[`HasBodyTracking`](https://developer.apple.com/documentation/realitykit/hasbodytracking)|
[`SpotLight`](https://developer.apple.com/documentation/realitykit/spotlight)|
[`DirectionalLight`](https://developer.apple.com/documentation/realitykit/directionallight)|[`HasDirectionalLight`](https://developer.apple.com/documentation/realitykit/hasdirectionallight)
[`PerspectiveCamera`](https://developer.apple.com/documentation/realitykit/perspectivecamera)|[`HasPerspectiveCamera`](https://developer.apple.com/documentation/realitykit/hasperspectivecamera)


## Has-protocols

protocol | underlying type, [`Component`](https://developer.apple.com/documentation/realitykit/component)
---|---
[`HasTransform`](https://developer.apple.com/documentation/realitykit/hastransform)|struct [`Transform`](https://developer.apple.com/documentation/realitykit/transform)
[`HasBodyTracking`](https://developer.apple.com/documentation/realitykit/hasbodytracking)|struct [`BodyTrackingComponent`](https://developer.apple.com/documentation/realitykit/bodytrackingcomponent)
[`HasSpotLight`](https://developer.apple.com/documentation/realitykit/hasspotlight)|[`SpotLightComponent`](https://developer.apple.com/documentation/realitykit/spotlightcomponent)<br/>[`SpotLightComponent.Shadow`](https://developer.apple.com/documentation/realitykit/spotlightcomponent/shadow)
[`HasDirectionalLight`](https://developer.apple.com/documentation/realitykit/hasdirectionallight)|[`DirectionalLightComponent`](https://developer.apple.com/documentation/realitykit/directionallightcomponent)<br/>[`DirectionalLightComponent.Shadow`](https://developer.apple.com/documentation/realitykit/directionallightcomponent/shadow)
[`HasPerspectiveCamera`](https://developer.apple.com/documentation/realitykit/hasperspectivecamera)|[`PerspectiveCameraComponent`](https://developer.apple.com/documentation/realitykit/perspectivecameracomponent)
[`HasCollision`](https://developer.apple.com/documentation/realitykit/hascollision)|[`CollisionComponent`](https://developer.apple.com/documentation/realitykit/collisioncomponent)
[`HasPhysicsBody`](https://developer.apple.com/documentation/realitykit/hasphysicsbody)|[`PhysicsBodyComponent`](https://developer.apple.com/documentation/realitykit/physicsbodycomponent)
[`HasPhysicsMotion`](https://developer.apple.com/documentation/realitykit/hasphysicsmotion)|[`PhysicsMotionComponent`](https://developer.apple.com/documentation/realitykit/physicsmotioncomponent)



## protocol [`Resource`](https://developer.apple.com/documentation/realitykit/resource) and its followers


[`AnimationResource`](https://developer.apple.com/documentation/realitykit/animationresource)  - [`AnimationPlaybackController`](https://developer.apple.com/documentation/realitykit/animationplaybackcontroller)
[`AudioResource`](https://developer.apple.com/documentation/realitykit/audioresource) - [`AudioPlaybackController`](https://developer.apple.com/documentation/realitykit/audioplaybackcontroller)
[`EnvironmentResource`](https://developer.apple.com/documentation/realitykit/environmentresource)
[`MeshResource`](https://developer.apple.com/documentation/realitykit/meshresource)
[`PhysicsMaterialResource`](https://developer.apple.com/documentation/realitykit/physicsmaterialresource)
[`ShapeResource`](https://developer.apple.com/documentation/realitykit/shaperesource)
[`TextureResource`](https://developer.apple.com/documentation/realitykit/textureresource)
