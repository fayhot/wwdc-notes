# [2018 601 Live Screen Broadcast with ReplayKit](https://developer.apple.com/videos/play/wwdc2018/601/)

ReplayKit

- Capture
  - Screen visuals
  - App audio
  - Microphone input
- Record and share
- Broadcast live
- HD quality capture
- Low latency
- Low performance impact
- Minimal power usage
- Privacy safeguards


### Agenda

Topic|Time|Page
---|---|---
Live Broadcast Overview | | p5
[System Broadcast Picker](2-system-broadcast-picker.md) | 835 | p22
[Developing Broadcast Extensions](3-developing-broadcast-extensions.md) | 1355 | p39
Protecting Content | 2510 | p65

## Live Broadcast Overview | | p5



### Live Broadcast

- Broadcast live to third party broadcast services
- Stream audio and visuals directly from device
- Provide commentary with microphone and camera (iOS) Content is secure and only accessible to the broadcast service


### Live Broadcast

- Usage examples
- Stream gameplay to Mobcrush or YouTube Mirror screen on a WebEx call
- Work with customer support via TeamViewerQS Stream a drawing app to Facebook


### In-App Broadcast

- Your app or game
  - Provides the content—visuals and audio Starts and stops the broadcast
- Broadcaster app
  - Provides sign-in and upload extensions Streams content to their network


### iOS System Broadcast

Broadcasts all onscreen activity (and sounds)
Start and stop from Control Center
Systemwide, continuous session
Home screen Moving app to app
Built-in to iOS 11 and above


## [Developing Broadcast Extensions](3-developing-broadcast-extensions.md) | | p39

For ReplayKit 2


## Protecting Content | 2510 | p65

UIScreen.isCaptured

- Prevent capturing of audio and video content of your app
- Stop media playback or displaying sensitive content
  - Check value of `UIScreen.captured`
  - Register for `UIScreenCapturedDidChangeNotification`
  - Check `UIScreen.screens.count` to allow screen mirroring


```swift
// Protecting content of your application from being captured
import UIKit
 
class func handleScreenCapturedChange() {
    let isScreenMirroring = UIScreen.screens.count > 1
    if (UIScreen.isCaptured && !isScreenMirroring) {
        // stop audio playback and remove sensitive content from the screen
    }
    
}
```
