
# [2016 231 CloudKit Best Practices](https://developer.apple.com/videos/play/wwdc2016/231/)

* Dave Browning CloudKit Engineer
* Nihar Sharma CloudKit Engineer

TOC

* How Apple uses CloudKit
* Using the CKOperation API
* Modeling your data
* Handling errors



## How Apple uses CloudKit

* Focus on building your app
* Automatic authentication
* Same data across all devices

### Use case

* iCloud is the source of truth
* Devices have a local cache
* CloudKit is the glue

### How Does It Work?

* On app launch
  * Fetch changes
  * Subscribe to future changes
* On push from CloudKit
  * Fetch changes

### Subscribe to Changes

```swift
if (subscriptionIslocallyCached) { return }
let subscription = CKDatabaseSubscription(subscriptionID: "shared-changes")
 let notificationInfo = CKNotificationInfo()
notificationInfo.shouldSendContentAvailable = true
subscription.notificationInfo = notificationInfo
```

### Push Config : Silent vs UI Push

```swift
let notificationInfo = CKNotificationInfo()
// Set only this property
notificationInfo.shouldSendContentAvailable = true
// The device does NOT need to prompt for user acceptance!
// Register for notifications via:
application.registerForRemoteNotifications(...)
```

### Listen for Pushes


### Fetch New Changes

## Using the CKOperation API

## Modeling your data


## [Handling errors](https://developer.apple.com/videos/play/wwdc2016/231/?time=2269)
