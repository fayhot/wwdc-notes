
# 2014 236 Building Interruptible and Responsive Interactions

[Video](https://developer.apple.com/videos/play/wwdc2014/236/)


Transitions

* Gesture to Animation
* Animation to Animation
* Animation to Gesture

## From Gesture to Animation [2]


### Computing Velocity
[UIPan​Gesture​Recognizer](https://developer.apple.com/reference/uikit/uipangesturerecognizer)
func velocity(in view: UIView?) -> CGPoint

[UIPinch​Gesture​Recognizer](https://developer.apple.com/reference/uikit/uipinchgesturerecognizer)
var velocity: CGFloat { get }

[UIRotation​Gesture​Recognizer](https://developer.apple.com/reference/uikit/uirotationgesturerecognizer)
var velocity: CGFloat { get }

### UIView's （Server-side render)??

### UIDynamicAnimator [7?]


### CADisplayLink [13]

### NSTimer, not a good option [14]

## From Animation to Animation, Andy Matuschak [17:48]

absolute (iOS 7 default)
BeginFromCurrentState
Additive (iOS 8 default)


### Additive Animations [25:50]

### Compatibility requirements

No Keyframe Animations
No pre-existing repeating animations
No pre-existing absolute animations

### Cancelling animations

```swift
circle.layer.removeAnimation(animation)
```

### Summary
Smoother transitions by default
Still use BeginFromCurrentState if unsure
Completion handlers may stack

## From Animation to Gesture, Josh Shaffer [33:30]

class func animate(withDuration duration: TimeInterval,
             delay: TimeInterval,
           options: UIViewAnimationOptions = [],
        animations: @escaping () -> Void,
        completion: ((Bool) -> Void)? = nil)

[UIView​Animation​Options](https://developer.apple.com/reference/uikit/uiviewanimationoptions)    

[allowUserInteraction](https://developer.apple.com/reference/uikit/uiviewanimationoptions/1622440-allowuserinteraction)


### Presentation Layer Hit Test


### Stop Animating [39:20]

```swift
let pos = view.layer.presentationLayer().position
view.center = pos
view.layer.removeAllAnimations() // the right animation.

### UIDynamicAnimator

```swift


```


## Transient Animation State [43]

## Demo, Andy Matuschak [44]

Toggle Bird


## Summary

* Use gesture velocity in animations
* Smoothly transition between animations
* Make animations interruptible
* Mind your state
