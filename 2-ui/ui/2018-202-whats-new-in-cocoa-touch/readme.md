
# [2018 202 What's New in Cocoa Touch](https://developer.apple.com/videos/play/wwdc2018/202)


2018-202-whats-new-in-cocoa-touch


- Josh Shaffer
- Eliza Block (Not show up?!)

- [Framework updates](1-framework-updates.md) | Josh Shaffer 
- API enhancements | Josh Shaffer| 2730 | p69
- Siri shortcuts|Josh Shaffer|3640|p97



## API enhancements | Josh Shaffer| 2730 | p69

## API enhancements (by frameworks)

- User Notifications 
- Messages | 2950 | p76
- Automatic Passwords and Security Code AutoFill
- Safe Area


### Messages | 2950 | p76

```xml
// New Info.plist key
<key>MSSupportedPresentationContexts</key>
<array>
<string>MSMessagesAppPresentationContextMessages</string>
<string>MSMessagesAppPresentationContextMedia</string>
</array>
```

```swift
var presentationContext: MSMessagesAppPresentationContext
 enum MSMessagesAppPresentationContext : UInt {
 case messages
 case media
 }
```



### Safe Area






## Siri shortcuts|Josh Shaffer|3640|p97

- NSUserActivity 
- Intents
  - SiriKit
  - Custom


### NSUserActivity

- Common API for Handoff and Spotlight
- Set eligibleForPrediction = true


