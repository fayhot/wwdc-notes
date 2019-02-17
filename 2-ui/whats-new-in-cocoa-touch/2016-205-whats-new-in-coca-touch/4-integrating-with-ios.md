## [Integrating with iOS](4-integrating-with-ios.md)| 4300 | p240


Keyboards Extensions
Automatically switch your multi-language keyboard extension based on text content
Add system Globe Key functionality  in your own keyboard extension

### Widgets - Display modes

- Widgets now have the concept   of “display modes”
- User-controlled
- Compact is fixed height
- Expanded is variable



### User Notifications

New Framework in iOS 10
Feature Parity
Unifies local and remote notification Better delivery management
In-app presentation option Multi-Platform


### User Notifications - Service extension

- Non-UI extension point Use cases
- Media attachments End-to-end encryption

## User Notifications - Content extension

- UI extension point Custom views
- No direct interaction
 

###  CallKit - Directory Extension

Blocking Identification

```swift
public class CXCallDirectoryExtensionContext : NSExtensionContext {
    public func addBlockingEntry(withNextSequentialPhoneNumber phoneNumber: String)
    public func addIdentificationEntry(
        withNextSequentialPhoneNumber phoneNumber: String,
        label: String)
}
```

### Call Provider API

- A 1st party experience for your VoIP application Full screen incoming call UI
- Integrated with other types of calls
VoIP calls appears in Favorites and Recents Supports Siri, CarPlay, Do Not Disturb, Bluetooth




### SiriKit



### Intents Extension

- Handle the interaction between  Siri and your application
  -  Intents and responses Intents are domain specific
  - Make sure Siri and your app agree on the request before performing it


```text
“Tell                   Miko on     WWDCChat    we need to meet after this session”

Send message intent     Recipient   App Name    Content
```

### IntentsUI Extension

Embed your own UI in the Siri Transcript

Optional


### Intents are Shared

- Intents describe requests
  - For Siri to communicate with your app
  - To integrate with CallKit
  - For Ride Sharing in Maps
  - To donate information to the system about a contact


iMessage Apps

- Write apps for Messages
- Sticker packs
- Messages extension

Sticker Packs
No code required
Package and distribute your images


Message Extensions
Dynamic stickers content Customize your UI
 


