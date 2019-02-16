

2018-233-adding-delight-to-your-ios-app


# [2018 233 Adding Delight to your iOS App](https://developer.apple.com/videos/play/wwdc2018/233/)

Six pro tips to make it magic

- Ben Fearnley, iOS System Experience
- Peter Hajas, iOS System Experience


• External Display Support
• Layout-Driven UI
• Laser-Fast Launches|2030|p183
• Smooth Scrolling
• Continuing with Continuity
• Debugging Like a Pro





Handling Connectivity
Is there an external display connected?

```swift
class var screens: [UIScreen]
if UIScreen.screens.count > 1 {
// External display is connected ...
}
```

What happens when the display is connected or disconnected?

- UIScreen.didConnectNotification
- UIScreen.didDisconnectNotification


if let externalScreen = UIScreen.screens.last {
    externalWindow = UIWindow()
    externalWindow.screen = externalScreen
    configureExternalWindow(externalWindow)
    externalWindow.isHidden = false
}

 
externalWindow.isHidden = true
externalWindow = nil

## Layout-Driven UI

### Recipe for Layout-Driven UI

- Find and track state that affects UI
- Dirty layout when state changes with setNeedsLayout()
- Update UI with state in layoutSubviews()


   Layout Animations Gestures
