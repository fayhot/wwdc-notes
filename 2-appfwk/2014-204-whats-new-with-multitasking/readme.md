
2014-204-whats-new-in-multitasking/readme.md


Keep app content fresh and interesting

- David Chan, iOS Software Engineering

- Multitasking in iOS 6 
  - Changes in iOS 7
- New Multitasking APIs
- Running in the background
  - Data Protection
  - Battery life
  - Cellular data usage


## Multitasking in iOS 6

- Background Task Completion 
- Background Audio
- Location Services
  - Region Monitoring
  - Significant Location Changes
  - Continuous Location Monitoring
- VoIP
- Newsstand

##  Changes to Existing Multitasking

- Background Task Completion 
- App Switcher
- Location Services
- Newsstand

```objc
task = [app beginBackgroundTaskWithExpirationHandler:^{
     task = UIBackgroundTaskInvalid;
 };
 // ...
[app endBackgroundTask:task];

```

Used for

- Encoding video
- Uploads or downloads
- Completing database operations

### Background Task Changes

Handling iOS 6 vs iOS 7

- If you were using background tasks for network transfers, use `NSURLSession` instead
- Switch between old and new mechanisms like this
 
```swift
if ([NSURLSession class]) {
    // Create a background session and enqueue transfers
}
else {
 // Start a background task and transfer directly 
}
```

In iOS 7

- Apps will no longer keep the device awake
- Apps will still get several minutes of runtime 
- Just not guaranteed to be contiguous



### App Switcher - Just click home twice

- New UI prominently features app snapshots
- Make sure your app looks good after the user leaves and comes back
  - State Restoration
- Swipe up to remove apps
  - Stop running in the background
- Updating snapshots in the background