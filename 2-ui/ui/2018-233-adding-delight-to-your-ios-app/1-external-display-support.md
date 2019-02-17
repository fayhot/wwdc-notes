
[External Display Support](1-external-display-support.md)

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