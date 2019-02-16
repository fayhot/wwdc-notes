
# [2016 707 Introduction to Notifications](Introduction to Notifications)




Notficiation Overview

User Notifictions

Registration / Content / Scheduling / Management / Actions

Service Extensions

### Remote

User facing

Silent update

* Feature parity
* Expanded content
* Same code path for local and remote notif handling
* Simplified delegate methods
* Better notification management.
* In-app presentation option.

Schedule and handle notification in extensions

Notification extensions!

Notification Delivery

Registration – get user authorization.

Subtitle, more dexterity


### Triggers

* Push
* Time Internal
* Calendar
* Location

### Scheduling

## Notification Handing

* Application in foreground
* In-app

## Notification Management

* Access
  * Pending Notifications
  * Delivered Notifications
* Remove Notifications
* Update and promote Notifications

Request Identifier


## Actions - J

* Default Action
* Custom Action
* Dismiss Action

### Actionable Notifications

Buttons with customizable title
Text input
Background or foreground
iOS and watchOS

#### Registration

```swift
let action = UNNotificationAction()


```


### Dismiss Action
```swift
let category =  UNNotificationCategory(identifier: actions: minimalActions: intentIdentifiers: options: [.customDismissAction])
```
## Handling


[`UNUserNotificationCenterDelegate`](https://developer.apple.com/reference/usernotifications/unusernotificationcenterdelegate)


```swift
optional func userNotificationCenter(_ center: UNUserNotificationCenter,
didReceive response: UNNotificationResponse,
withCompletionHandler completionHandler: @escaping () -> Void)
```


## Service Extensions [31]

Non UI iOS Extension

### Potential uses

End-to-end encryption / add attachments

Service Extension . Xcode

[`UINotificationServiceExtension`](https://developer.apple.com/reference/usernotifications/unnotificationserviceextension)



```swift
class NotifSvc : UINotificationServiceExtension {

  override func didReceive(_ request: UNNotificationRequest,
  withContentHandler contentHandler: @escaping (UNNotificationContent) -> Void) {

  }

}
```
### Example payload
```json
{aps: {mutable-content : 1 },

encrypted-content: “”

}
```

## Summary

* Notifications Overview
* User
  * Registration
  * Content
  * Scheduling
  * Management
  * Actions
* Service Extensions
