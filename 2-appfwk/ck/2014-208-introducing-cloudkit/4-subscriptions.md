4-subscriptions.md

## Subscriptions

- CKSubscription
- Combine a RecordType, a NSPredicate, and Push
- Push via Apple Push Service
- Augmented payload



### Creating

```objc
NSPredicate *predicate = [NSPredicate predicateWithFormat:
                          @"start > %@", [NSDate date]];
CKSubscription *subscription = [[CKSubscription alloc]
       initWithRecordType:@"Party"
                predicate:predicate
                  options:CKSubscriptionOptionsFiresOnRecordCreation];

CKNotificationInfo *notificationInfo = [CKNotificationInfo new];
notificationInfo.alertLocalizationKey = @"LOCAL_NOTIFICATION_KEY";
notificationInfo.soundName = @"Party.aiff";
notificationInfo.shouldBadge = YES;

subscription.notificationInfo = notificationInfo;
```


### Saving

```objc
CKSubscription *subscription = ...;
[[publicDatabase saveSubscription:subscription
   completionHandler:^(CKSubscription *subscription, NSError *error) {
    // labor-of-love error handling when (error != nil)
}];
```

### Handling push

```objc
@implementation AppDelegate

- (void)application:(UIApplication *)application
                    didReceiveRemoteNotification:(NSDictionary *)userInfo {
    
    CKNotification *cloudKitNotification = [CKNotification
                    notificationFromRemoteNotificationDictionary:userInfo];
    NSString *alertBody = cloudKitNotification.alertBody;
    if (cloudKitNotification.notificationType == CKNotificationTypeQuery) {
        CKQueryNotification *queryNotification = cloudKitNotification;
        CKRecordID *recordID = [queryNotification recordID];
    } 
}
```

> It should be ` func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void)`

