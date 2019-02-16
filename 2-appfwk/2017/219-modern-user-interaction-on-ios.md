
# [219 Modern User Interaction on iOS](https://developer.apple.com/videos/play/wwdc2017/219/)


* The UIGestureRecognizer system
* System gesture interaction
* Playing nice with Drag and Drop


## Basics

* [Touches, Presses, and Gestures](https://developer.apple.com/documentation/uikit/touches_presses_and_gestures)
  * UITouch
  * UIGestureRecognizer



```swift
// Influencing responder based touch handling
class UIGestureRecognizer : NSObject {
open var delaysTouchesEnded: Bool // default is true.
open var cancelsTouchesInView: Bool // default is true.
open var delaysTouchesBegan: Bool // default is false.

}
```    
## Exclusion
```swift
public protocol UIGestureRecognizerDelegate : NSObjectProtocol {
}
open class UIGestureRecognizer : NSObject {
optional public func
_
gestureRecognizer( gestureRecognizer: , shouldRecognizeSimultaneouslyWith otherGestureRecognizer: ) -> Bool
UIGestureRecognizer UIGestureRecognizer

  }
```
## Failure Requirements


```swift
// Failure Requirements
class UIGestureRecognizer : NSObject {
open func require(toFail otherGestureRecognizer: UIGestureRecognizer)
}

public protocol UIGestureRecognizerDelegate : NSObjectProtocol {
optional public func gestureRecognizer(_ gestureRecognizer: UIGestureRecognizer, shouldRequireFailureOf otherGestureRecognizer: UIGestureRecognizer) -> Bool
optional public func gestureRecognizer(_ gestureRecognizer: UIGestureRecognizer, shouldBeRequiredToFailBy otherGestureRecognizer: UIGestureRecognizer) -> Bool
}
```

subclasses

```swift

open class UIGestureRecognizer : NSObject {
open func shouldRequireFailure(of otherGestureRecognizer: UIGestureRecognizer) -> Bool
open func shouldBeRequiredToFail(by otherGestureRecognizer: UIGestureRecognizer) -> Bool }
```

### Hit Testing


### Custom UIGestureRecognizers

* Begin late and fail fast!
* Ignore touches `ignore(_ touch:, for event:)`
* Don’t forget `touchesCancelled(\_:with:)`


## System Gesture Interaction - by Glen Low


### Speaking in Tongues

In class MyViewController: UIViewController

```swift
// override to return which screen edges to defer system gestures
override func preferredScreenEdgesDeferringSystemGestures() -> UIRectEdge { return deferControlCenter ? .bottom : UIRectEdge()
}

// call whenever your method would return a different screen edge
var deferControlCenter : Bool {
didSet { setNeedsUpdateOfScreenEdgesDeferringSystemGestures() }
}
```

### For Containers Only

### Don’t Do It, Because...

* Don’t mess with the familiar
* Your recognizers may already get the touches
* Telling us ≠ us doing it
* Your app is only used casually


## Playing Nice With Drag and Drop - Michael Turner


### initiating a Drag

### Long Press and Move

UILongPressGestureRecognizers   are delayed

A beginning drag will  cancel the touch

Long presses are delayed until the touch ends

### Long Press and Lift

### Adding to a Drag
