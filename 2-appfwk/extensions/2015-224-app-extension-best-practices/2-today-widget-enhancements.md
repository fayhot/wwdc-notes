[Today widget enhancements](2-today-widget-enhancements.md) |  Ian Baird | x | p105





### Staying Responsive

Locking in the shared container

- Be careful taking exclusive locks for data in the shared container
- Extension killed if it’s suspended while holding an exclusive lock


Task assertions

- Extensions suspended when no longer in use
- Protect serialization and other clean-up tasks with background task assertions


```swift

let pi = NSProcessInfo.processInfo()
pi.performExpiringActivityWithReason("clean-up")  { expired in
    if (!expired) {
        self.serializeData()
    } else {
        self.cleanupSerializingData()
    } 
}
```



### Task assertions

- Released when your code exits the block
- Re-entrant execution of callback for expiration
- Task assertions are not always available for your extension

### Working with other queues

- Task assertion scoped to callback block
- Callback block must synchronize with protected work on other queues
- Example
  - Dispatch block to the main queue

### Staying Up to Date

Darwin Notification Center

- Similar to NSNotificationCenter
- Small number of use-cases
- Example
  - Hint to your extension to reload the model

### Containing app API

```swift
let nc = CFNotificationCenterGetDarwinNotifyCenter()
CFNotificationCenterPostNotification(nc,
  "com.example.app-model-updated",
  nil,
  nil,
  CFBooleanGetValue(true))
```

### Extension API

```swift
let nc = CFNotificationCenterGetDarwinNotifyCenter()
CFNotificationCenterAddObserver(nc,
  nil,
  { _ in self.reloadModel() },
  "com.example.app-model-updated",
  nil,
  .DeliverImmediately)
```  