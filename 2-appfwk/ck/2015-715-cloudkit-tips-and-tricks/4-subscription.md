

## [Subscriptions](4-subscription.md) | | p 169
(https://developer.apple.com/videos/play/wwdc2015/715/?time=2084) 



### Setup

* APS capability managed from Developer Portal
* aps-environment entitlement
* Registration via UIApplication   
  * registerForRemoteNotifications()
  * registerUserNotificationSettings(notificationSettings:   UIUserNotificationSettings)


### Push Priorities

1. Remote notification background mode

Under "Background Modes", tick "Remote notifications"

2. UIApplication

```swift
func application(application: UIApplication,  
    didReceiveRemoteNotification: [NSObject : AnyObject],
    fetchCompletionHandler: (UIBackgroundFetchResult) -> Void) {
    
    ...
}
```

3. [`CKNotificationInfo`](https://developer.apple.com/reference/cloudkit/cknotificationinfo)


[`CKFetchNotificationChangesOperation`](https://developer.apple.com/reference/cloudkit/ckfetchnotificationchangesoperation)



Silent Push Notifications

- System opportune time
- Push delivery is best-effort
  - May get dropped or coalesced


Sync notification collection
  
CKFetchNotificationChangesOperation

Background task API:


```swift
class UIApplication : UIResponder {
    func beginBackgroundTaskWithName(taskName: String?,
        expirationHandler: (() -> Void)?) -> UIBackgroundTaskIdentifier

}

```


### Interactive Notifications



