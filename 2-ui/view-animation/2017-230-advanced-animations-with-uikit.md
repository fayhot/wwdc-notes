
# [230 Advanced Animations with UIKit](https://developer.apple.com/videos/play/wwdc2017/230/)


* Basics
* Interactive and Interruptible Animations
* New Property Animator behaviors
* Coordinating Animations
* Tips and Tricks


## Basics

### UIView-based Animations

```swift
UIView.animate(withDuration:){

}
```

## Interactively Animating

```swift
var animator: UIViewPropertyAnimator!
func handlePan(recognizer: UIPanGestureRecognizer) {
    switch recognizer.state {
    case .began:
        animator = UIViewPropertyAnimator(duration: 1, curve: .easeOut, animations: {
            circle.frame = circle.frame.offsetBy(dx: 100, dy: 0)
})
        animator.pauseAnimation()
    case .changed:
        let translation = recognizer.translation(in: circle)
        animator.fractionComplete = translation.x / 100
    case .ended:
        animator.continueAnimation(withTimingParameters: nil, durationFactor: 0)
    }
}
```

### Time Conversion

Pause and Continue

## Interruptible Animation

```swift
func animateTransitionIfNeeded(duration: TimeInterval) {...}
var progressWhenInterrupted: CGFloat = 0
func handlePan(recognizer: UIPanGestureRecognizer) {
    switch recognizer.state {
    case .began:
        animateTransitionIfNeeded(duration: 1)
        animator.pauseAnimation()
        progressWhenInterrupted = animator.fractionComplete
    case .changed:
        let translation = recognizer.translation(in: circle)
        animator.fractionComplete = (translation.x / 100) + progressWhenInterrupted
    case .ended:
        let timing = UICubicTimingParameters(animationCurve: .easeOut)
        animator.continueAnimation(withTimingParameters: timing, durationFactor: 0)
   }
}


```

## New Animator Behaviors

var scrubsLinearly: Bool
var pausesOnCompletion: Bool



## Coordinating Animations


Build a fully interactive, interruptible animated transition
Coordinate across multiple uniquely timed animators
