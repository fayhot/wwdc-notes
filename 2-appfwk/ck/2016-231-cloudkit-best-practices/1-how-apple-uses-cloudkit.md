
## [How Apple uses CloudKit](1-how-apple-uses-cloudkit.md) | Dave Browning 

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



let operation = CKModifySubscriptionsOperation(subscriptionsToSave: [subscription],
   subscriptionIDsToDelete: [])

operation.modifySubscriptionsCompletionBlock = { ...
   if error != nil { } // Handle the error
   else { self.subscriptionIslocallyCached = true }
}

operation.qualityOfService = .utility
self.sharedDB.add(operation)


```

### Listen for Pushes

```swift
// Listen for pushes
func application(_ application: UIApplication,
   didReceiveRemoteNotification userInfo: [NSObject : AnyObject],
   fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
   
    let dict = userInfo as! [String: NSObject]
    let notification = CKNotification(fromRemoteNotificationDictionary: dict)
    if (notification.subscriptionID == "shared-changes") {
        fetchSharedChanges {
         completionHandler(UIBackgroundFetchResult.newData)
        }
    } 
}
```
### Fetch New Changes

```swift
// Fetching database changes after a push
func fetchSharedChanges(_ callback: () -> Void) {
    let changesOperation = CKFetchDatabaseChangesOperation(
        previousServerChangeToken: sharedDBChangeToken) // previously cached
    
    changesOperation.fetchAllChanges = true
    changesOperation.recordZoneWithIDChangedBlock = { ... } // collect zone IDs
    changesOperation.recordZoneWithIDWasDeletedBlock = { ... } // delete local cache
    changesOperation.changeTokenUpdatedBlock = { ... } // cache new token
    changesOperation.fetchDatabaseChangesCompletionBlock = {
      (newToken: CKServerChangeToken?, more: Bool, error: NSError?) -> Void in
      // error handling here
      self.sharedDBChangeToken = newToken // cache new token
      self.fetchZoneChanges(callback) // using CKFetchRecordZoneChangesOperation
    }
    self.sharedDB.add(changesOperation)
}
```
