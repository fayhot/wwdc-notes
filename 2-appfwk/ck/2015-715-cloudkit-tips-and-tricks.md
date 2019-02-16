
# [2015 715 CloudKit Tips and Tricks](https://developer.apple.com/videos/play/wwdc2015/715/)

* error handling
* local cache
* subscriptions
* performance


## error handling

### account


static let CKAccountChanged: NSNotification.Name



### retry


### handing conflicts .



cloud kit operation


query [23]

limit (say 20 per page)

thumbnail = desiredKeys


## Storing Data Locally [30?]

How do we fetch changes from our custom zone in order to keep that cache up to date? [34:10]

When do we use ChangeOperation..  - Anser : Subscription .


## [Subscriptions](https://developer.apple.com/videos/play/wwdc2015/715/?time=2084)

### Setup

* APS capability managed from Developer Portal
* aps-environment entitlement
* Registration via UIApplication   
  * registerForRemoteNotifications()
  * registerUserNotificationSettings(notificationSettings:   UIUserNotificationSettings)


### Push Priorities

1. Remote notification background mode

2. UIApplication

```swift
func application(application: UIApplication,  didReceiveRemoteNotification: [NSObject : AnyObject],
fetchCompletionHandler: (UIBackgroundFetchResult) -> Void) {  ...
}
```

3. [`CKNotificationInfo`](https://developer.apple.com/reference/cloudkit/cknotificationinfo)


[`CKFetchNotificationChangesOperation`](https://developer.apple.com/reference/cloudkit/ckfetchnotificationchangesoperation)

## CloudKit Performance Tips


### Managing Dependent Tasks

#### Don't: Nesting convenience API calls

#### Don't: Making operations synchronous

#### Do: NSOperation dependencies

### NSOperation Quality of Service



## Summary

* Error handling is vital
* Batch requests
* Schema trade-offs
* Configure CKOperations for performance
