2018-235-uikit-apps-for-every-size-and-shape

# [2018 235 UIKit: Apps for Every Size and Shape](https://developer.apple.com/videos/play/wwdc2018/235)


- David Duncan, UIKit Engineer
- Tyler Fox, UIKit Engineer
- Russell Ladd, UIKit Engineer


Topic|Speaker|Time|Page
---|---|---|---
Safe area and layout margins|David Duncan||p8
Scroll views|Tyler Fox|1250|p68
Building adaptive apps|Russell Ladd|2655|p99


```swift
class UIScrollView : UIView {
    var contentInsetAdjustmentBehavior: UIScrollView.ContentInsetAdjustmentBehavior
}
```

[`UIScrollView.ContentInsetAdjustmentBehavior`](https://developer.apple.com/documentation/uikit/UIScrollView/ContentInsetAdjustmentBehavior) iOS 11

case | description
---|---
automatic|Automatically adjust the scroll view insets.
scrollableAxes|Adjust the insets only in the scrollable directions.
never|Do not adjust the scroll view insets.
always|Always include the safe area insets in the content adjustment.




## Building adaptive apps|Russell Ladd|2655|p99


tableView.cellLayoutMarginsFollowReadableWidth = true


tableView.insetsContentViewsToSafeArea = true


### bottom padding when safe area is zero

constraint 1: bottom = bottom + constant , not required

constraint 2: safe area of view against safe area of its parent view.

