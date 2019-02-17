[Adopting system features](3-adapting-system-features.md) | 3150 | p170



[Adopting system features](3-adapting-system-features.md) | 3150 | p170

Opening applications
Improving openURL
Asynchronous, with a completion handler
 •
Let you check if a handler app is installed for
•
universal links

```swift
UIApplication.shared().
   open(url, options: [UIApplicationOpenURLOptionUniversalLinksOnly: true]) {
      (didOpen: Bool) in
         if !didOpen {
            // No application available
        } 
    }
```


Core Data

- Query generations
- Concurrency improvements
- Tooling improvements


CloudKit (NEW)

- Public databases
- Private, per user databases
- Record sharing

CloudKit

UICloudSharingController

- Managing the invitation flow
- Private and secure

```swift
let sharingController = UICloudSharingController(share: share, container: self.container)
```

> [2016 ??? What’s New with CloudKit]()


NSUserActivity | 3615 |  

- Capture the state of your application
- Infrastructure for Handoff, Spotlight, ... 
- Now supports locations
- `activity.mapItem = myLocation`

Increase Usage of Your App With Proactive Suggestions


App Search

In iOS 9, we added support for indexed activities and indexed content

```swift
let userActivity = NSUserActivity(activityType: "myActivityType")
userActivity.eligibleForSearch = true
userActivity.eligibleForPublicIndexing = true
userActivity.title = "Presenting What’s New in Cocoa Touch"
let attributes = CSSearchableItemAttributeSet(itemContentType: "public.item")
attributes.displayName = ...
userActivity.contentAttributeSet = attributes
```

Add a CoreSpotlightContinuation key in your Info plist Implement a new UIApplicationDelegate method

```swift
func application(application: UIApplication,
                 continueUserActivity userActivity: NSUserActivity,
                 restorationHandler: ([AnyObject]?) -> Void) -> Bool {
    if userActivity.activityType == CSQueryContinuationActionType {
        if let searchQuery = userActivity.userInfo?[CSSearchQueryString] as? String {
         // Search
        }
        return true
    }
    return false
}
```

CSSearchQuery

- Search the data you’ve already indexed with Spotlight
- Great power and performance, full content search
- Powerful query syntax

```swift
let query = CSSearchQuery(queryString: queryString, attributes: ["displayName"])
query.foundItemsHandler = {
   (items: [CSSearchableItem]) in
      /* process received items */
}
query.start()
```



ReplayKit
RPBroadcastActivityViewController
Now supports live broadcasting Third-party services support

SceneKit
New realistic rendering
Physically-based rendering High dynamic range Linear color space

Apple Pay
Apple Pay in UI code Apple Pay in Safari
Also available in SFSafariViewController Apple Pay in non-UI extensions
Great feature for your iMessage apps