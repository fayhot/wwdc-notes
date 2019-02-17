
## [Layout-Driven UI](2-layout-driven-ui.md) | | p41

### Recipe for Layout-Driven UI

- Find and track state that affects UI
- Dirty layout when state changes with setNeedsLayout()
- Update UI with state in layoutSubviews()


   Layout Animations Gestures

Animation API

- UIViewPropertyAnimator
- UIView closure API

> [2017 230 Advanced Animations with UIKit](https://developer.apple.com/videos/play/wwdc2017/230/)


Animations with Layout-Driven Updates

.beginFromCurrentState


```swift
var cardsInDeck = [CardView]() {
    didSet {
        setNeedsLayout()
    }
}
func putCardInDeck(_ card: CardView) {
    cardsInDeck.append(card)
    UIView.animate(withDuration: 0.3,
                   delay: 0,
                   options: [.beginFromCurrentState],
                   animations: {
                    self.layoutIfNeeded()
    }, completion: nil)
}
```

### Gestures

UIGestureRecognizer


### Discrete Gestures

Possible -> Recognized

### Continuous Gestures

Possible -> Began -> Changed -> Ended

### UIPanGestureRecognizer

- Use translationInView() for dragging
- Use velocityInView() for animation handoffs

Building Interruptible and Responsive Interactions