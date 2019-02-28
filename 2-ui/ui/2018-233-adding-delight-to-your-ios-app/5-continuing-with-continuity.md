### [Continuing with Continuity](5-continuing-with-continuity.md) | 3255 | p127



### A Magical Experience

- Seamlessly transition activities between devices
- Works between iOS, macOS, and watchOS
- Doesn’t require an Internet connection
- It’s easy to set up!


### How could you use Handoff?


Messages / Documents / Photos


### [`NSUserActivity`](https://developer.apple.com/documentation/foundation/nsuseractivity)

Originating Device

```swift
let activity = NSUserActivity(activityType:"com.apple.developer.video")
activity.title = "Adding Delight to your iOS App"
activity.isEligibleForHandoff = true
activity.userInfo = ["session-id" : "2018-223", "currentTime" : 2340]
userActivity = activity
```


Continuing device

- App must declare support for activity type
- Implement these UIApplicationDelegate functions
  - application(_:willContinueUserActivityWithType:)
  - application(_:continue:restorationHandler:)


### Continuation Streams

- Set supportsContinuationStreams to true
- Call on the continuing device
  - getContinuationStreams(completionHandler:)
- Call back on the originating device
  - userActivity(_:didReceive:outputStream:)

> Stream Programming Guide developer.apple.com

### Document-Based Apps

- Get this for free!
- [`UIDocument`](https://developer.apple.com/documentation/uikit/uidocument)/`NSDocument` automatically create [`NSUserActivity`](https://developer.apple.com/documentation/foundation/nsuseractivity) objects
- Supports documents in iCloud
- Configure your Info.plist

### Native App-to-Web Browser Handoff

- Set webpageURL property on the user activity


### Web Browser-to-Native App Handoff

- Configure list of approved app IDs on web server
- Continuing app must opt in with an associated-domains entitlement
  
>  2014 Adopting Handoff on iOS and OS X 

### Continuing with Continuity

- Implement Handoff
- Delight your users
- Integrate with Spotlight search, Siri Shortcuts, and more

> 2015 Introducing Search APIs
> 2018 Introduction to Siri Shortcuts
