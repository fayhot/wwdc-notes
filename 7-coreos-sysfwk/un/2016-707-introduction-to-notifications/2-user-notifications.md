2-user-notifications.md



Notification Delivery


Registration – get user authorization.

Token Registration

## Content

Subtitle, more dexterity

[`UNNotificationContent`](https://developer.apple.com/documentation/usernotifications/unnotificationcontent) 

[`UNMutableNotificationContent`](https://developer.apple.com/documentation/usernotifications/unmutablenotificationcontent)

UNNotificationAttachment





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

- Buttons with customizable title
- Text input
- Background or foreground
- iOS and watchOS

#### Registration

```swift
let action = UNNotificationAction()


```


### Dismiss Action
```swift
let category =  UNNotificationCategory(
  identifier: 
  actions: 
  minimalActions: 
  intentIdentifiers: 
  options: [.customDismissAction])
```
## Handling


[`UNUserNotificationCenterDelegate`](https://developer.apple.com/reference/usernotifications/unusernotificationcenterdelegate)


```swift
optional func userNotificationCenter(_ center: UNUserNotificationCenter,
didReceive response: UNNotificationResponse,
withCompletionHandler completionHandler: @escaping () -> Void)
```