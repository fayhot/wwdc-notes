
## Hidden Notification Content

Privacy

What’s new

- Extended support to all apps
- Global setting
- Settings per app
- API to customize notification content


```swift 
// Hidden Notification Content
let commentCategory = UNNotificationCategory(
    identifier: "comment-category",
    actions: [],
    intentIdentifiers: [], 
    hiddenPreviewsBodyPlaceholder: "Comment")
```


Pluralization


```swift 
let placeholder =  NSString.localizedUserNotificationString(forKey:”COMMENT_KEY”, arguments: nil)

let commentCategory = UNNotificationCategory(
    identifier: "comment-category", actions: [],
    intentIdentifiers: [], 
    hiddenPreviewsBodyPlaceholder:placeholder
)
```

---

```swift
// Hidden Notification Content
let commentCategory = UNNotificationCategory(
    identifier: "comment-category", actions: [],
    intentIdentifiers: [], 
    hiddenPreviewsBodyPlaceholder:
NSString.localizedUserNotificationString(forKey:”COMMENT_KEY”,arguments: nil)
)

let imageCategory = UNNotificationCategory(
    identifier: "image-category", actions: [],
    intentIdentifiers: [], 
    hiddenPreviewsBodyPlaceholder:
NSString.localizedUserNotificationString(forKey:”IMAGE_KEY", arguments: nil))
```

---

```swift
let commentCategory = UNNotificationCategory(
    identifier: "comment-category", actions: [],
    intentIdentifiers: [], 
    hiddenPreviewsBodyPlaceholder:
NSString.localizedUserNotificationString(forKey:”COMMENT_KEY”,  arguments: nil),
    options: [.hiddenPreviewsShowTitle])

```

Best practices

- User defined setting
- Retrieve settings using `showPreviewsSetting`
- Thread identifiers
- Pluralization
