


## Customizing Rich Notifications | Kritarth Jain | 2415 | p158

### Motivation

- App specific look and feel
- Custom display of notification content
- Interactive and dynamic UI

### Content Extensions


### Content Extension Template


### Content Extension Info.plist

### Code

```swift
// Content Extension Custom UI
class NotificationViewController: UIViewController, UNNotificationContentExtension {
    var videoPlayer: AVPlayer?
    func didReceive(_ notification: UNNotification) {
        let content = notification.request.content
        if let attachment = content.attachments.first {
            if attachment.url.startAccessingSecurityScopedResource() {
                videoPlayer = AVPlayer(url: attachment.url)
                attachment.url.stopAccessingSecurityScopedResource()
            }
        }
    }
}
```

### Code 

```swift 
// Content Extension Custom UI
class NotificationViewController: UIViewController, UNNotificationContentExtension {
    @IBOutlet var userLabel: UILabel?
    @IBOutlet var locationLabel: UILabel?
    @IBOutlet var descriptionLabel: UILabel?
    func didReceive(_ notification: UNNotification) {
        let content = notification.request.content
        self.title = content.title
        
        let userInfo = content.userInfo
        self.userLabel?.text = userInfo["video-user"] as? String
        self.locationLabel?.text = userInfo["video-location"] as? String
        self.descriptionLabel?.text = userInfo["video-description"] as? String
    }
}
```

### Content Extension size ratio


### Best practices

- Custom UI elements
- Display all relevant information
- Reuse app view controllers
- Correct sizing
- Fast loading and layout
