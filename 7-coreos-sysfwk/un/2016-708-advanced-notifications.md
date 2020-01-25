
# [2016 708 Advanced Notifications](https://developer.apple.com/videos/play/wwdc2016/708/)

* Notifications User Interface
* Media Attachments
* Customization

## Notifications User Interface

iOS | Features
--|--
8 | actions for UI Notification
9 | quick reply.
10 | press notification to show more details.


## Media attachments

UNNotificationServiceExtension

func didReceive(_ request: UNNotificationRequest, withContentHandler contentHandler: @escaping (UNNotificationContent) -> Void)

func serviceExtensionTimeWillExpire()


### Media Attachments

* Local and Remote
* Image, Audio and Video
* Download in the service extension
  * Limited processing time and size
* Add attachment to notification
  * File is moved and managed by the system
* Supports Gifs


## Custom UI [9]

[`UserNotificationsUI`](https://developer.apple.com/reference/usernotificationsui)

[`UNNotificationContentExtension`](https://developer.apple.com/reference/usernotificationsui/unnotificationcontentextension)

### Notification Content Extension





```swift
class NotificationViewController : UIViewController, UNNotificationContentExtension {

  func didReceived(_ notification : UINotification) {

  }

}
```

#### Info.plist

* NSExtension -
  * NSExtensionAttributes
    *   UNNotificationExtensionDefaultContentHidden
    * UNNotificationExtensionCategory
      * array
    * UNNotificationExtensionInitialContentSizeRatio

See [Information Property List Key Reference](https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/AppExtensionKeys.html#//apple_ref/doc/uid/TP40014212-SW1)

preferredContentSize , or AutoLayout, Storyboard

## Actions [20]

### Intercepting Action Response

* Delivered to the extension
* Can delay dismissal

```swift
optional func didReceive(_ response: UNNotificationResponse,
completionHandler completion: @escaping (UNNotificationContentExtensionResponseOption) -> Void)

```

### Text Input Action [23]

```swift
var inputAccessoryView : UIView {

}



```

## Summary

* Attachments and custom UI
* Attachments with service extension
* Custom UI with content extension
  * Media attachments
  * User interaction


The End [27]
