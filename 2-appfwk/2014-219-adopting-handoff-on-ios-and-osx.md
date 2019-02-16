
# [2014 219 Adopting Handoff on iOS and OS X](https://developer.apple.com/videos/play/wwdc2014/219/)

[ASCIIwwdc](http://asciiwwdc.com/2014/sessions/219)

## TOC (What You Will Learn)

* What is Handoff
* Adopting Handoff in your app
* In-depth Handoff adoption

## What is Handoff [2] (Michael Jurewitz)


### Adopting Handoff [5]

* _Decide_ which activities to support in your app
* _Create_ activities in specific parts of your app
* _Handle_ continuing incoming activities in your app


API

* [`NSUserActivity`](https://developer.apple.com/reference/foundation/nsuseractivity)
* `let NSUserActivityTypeBrowsingWeb: String`
* [`NSUserActivityDelegate`](https://developer.apple.com/reference/foundation/nsuseractivitydelegate)


### Additional Handoff Support [9]

* Streams between applications in two devices
* Handoff between native app and website you own


### Agenda

* AppKit and UIKit support for adopting Handoff
* Working with NSUserActivity directly
* Native app to website Handoff
* Using continuation streams between apps

## Adopting Handoff in Your App (Vince Spader) [10]

### Creating User Activities

NSDocument, UIDocument, NSResponder and UIResponder now have:

```swift
NSUserActivity *userActivity = [[NSUserActivity alloc]  initWithActivityType:@“com.company.viewing-message”];
userActivity.title = @“Viewing Message”;   
document.userActivity = userActivity;
```

Add NSUbiquitousDocumentUserActivityType to each CFBundleDocumentTypes entry, in Info.plist

#### becomeCurrent on iOS

#### becomeCurrent on OS X

### Updating User Activities

#### Documents and Responders

`userInfo`



[`UIResponder`](https://developer.apple.com/reference/uikit/uiresponder)



[`UIDocument`](https://developer.apple.com/reference/uikit/uidocument)



[`UIApplicationDelegate`](https://developer.apple.com/reference/uikit/uiapplicationdelegate)


### Continuing User Activities

#### AppDelegate

Step 1

optional func application(_ application: UIApplication,
willContinueUserActivityWithType userActivityType: String) -> Bool

Step 2

optional func application(_ application: UIApplication,
                 continue userActivity: NSUserActivity,
       restorationHandler: @escaping ([Any]?) -> Void) -> Bool


##### Document-based app


## NSUserActivity In-depth (Keith Stattenfield) [32]

### Non AppKit/UIKit uses

### Activity Type Strings

### Advanced NSUserActivity

```swift
activity.delegate = self
activity.needsSave = true

willSave( _ )
```
```swift
wasContinued( _ )
```

### Website Handoff [42]


#### Native application to Web browser

#### Web browser to native application

com.apple.developer.associated-domains , in info.plist

### Continuation Streams

* Need more than a one-way, one time exchange of data from creator to receiver
* Establishes a bidirectional stream for some kind of interactive purposes

```swift
NSUserActivity* activity = [[NSUserActivity alloc] initWithActivityType: @“com.company.interact” ];
activity.userInfo = @{ ... }
activity.delegate = self; activity.supportsContinuationStreams = YES; [activity becomeCurrent ];
```

#### NSUserActivity, on the receiving device

```swift
-(void) userActivity:(NSUserActivity *)userActivity
didReceiveInputStream:(NSInputStream *)inputStream outputStream:
(NSOutputStream *)outputStream {
... }
```

## So, you've learned [49]

* AppKit/UIKit support
* NS/UIDocument support
* Continuation streams
* Website interoperability

[Handoff Programming Guide](https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/Handoff/HandoffFundamentals/HandoffFundamentals.html#//apple_ref/doc/uid/TP40014338)

Related Sessions

* ??? Cloud Documents
* [506 Your App, Your Website, and Safari](https://developer.apple.com/videos/play/wwdc2014/506/)
