# [2015 510 What's New in Core Image](https://developer.apple.com/videos/play/wwdc2015/510/)


* David Hayward Engineering Manager
* Tony Chu Engineer
* Alexandre Naaman Lead Engineer

No|Topic|Presenter|Time|Page
--|--|--|--|--
1|A Brief Introduction to Core Image
2|What’s New in Core Image|David|405
3|Bridging Core Image with Other Frameworks||1315


## What’s New in Core Image - 405



* Metal
* Filters
* Detectors
* Color management
* Kernel class and language
* Unified implementation


### Metal Integration


### Improved CIKernel Language (OS X)


The Goal of the CIKernel Language
Write kernels once and run everywhere regardless of:
System: iOS or OS X
Size: destCoord() and samplerTransform() enable automatic tiling Renderer: Metal, OpenCL, OpenGL, OpenGL ES

## Core Image and Metal - Tony - 1405

## Core Image Provider - Alex - 2610

## View Class and Core Image - 2820


### Core Image and CALayer

### Core Image and IOSurface - 3155

### SpriteKit - 3315

### SceneKit - 3505

Filter properties on are animatable with Core Animation

```swift
let animation = CABasicAnimation(keyPath:  "filters.\(pixellate.name).\(kCIInputScaleKey)")
    animation.toValue = 50
    animation.fromValue = 0
    animation.autoreverses = true
    animation.repeatCount = FLT_MAX
    animation.duration = 2.0
animation.timingFunction = CAMediaTimingFunction(name:  kCAMediaTimingFunctionEaseInEaseOut)
    ship.addAnimation(animation, forKey: nil)
```
