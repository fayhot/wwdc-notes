# [2015 224 App Extension Best Practices](https://developer.apple.com/videos/play/wwdc2015/224/)

- Sophia Teutschler, UIKit Engineer
- Ian Baird, CoreOS Engineer

Topic|Speaker|Time|Page
---|---|---|---
Action and Share Extensions
[Today widget enhancements](2-today-widget-enhancements.md) |  Ian Baird | x | p105
Real world examples

Background Refresh | |3330 | p188

### Updating the widget

- System opportunistically refreshes content
- View controller conforms to NCWidgetProviding
- Implements update delegate method
 
```swift
func widgetPerformUpdateWithCompletionHandler(completionHandler:
((NCUpdateResult) -> Void)) {
  let updated = refreshTheModel()
  if (updated) { view.setNeedsDisplay() }
  completionHandler(updated ? .NewData : .NoData)
}
```

## Networking | | 3630 | p204

NSURLSession

- Background sessions
- Task performed by the system
- Updates delivered to your extension   as long as it stays alive
- Error and event handled by the   containing app



### Extension API 

```swift
let sc = NSURLSessionConfiguration.backgroundSessionConfigurationWithIdentifier(
  "com.example.my-download-session")
sc.sharedContainerIdentifier = "group.com.example.my-app"
let session = NSURLSession(configuration: sc, delegate: self, delegateQueue:
NSOperationQueue.mainQueue())
let request = NSURLRequest(URL: NSURL(string: "https://www.apple.com/")!)
let task = session.downloadTaskWithRequest(request)
task?.resume()
```


Containing app API

```swift
func application(application: UIApplication,
  handleEventsForBackgroundURLSession identifier: String,
  completionHandler: () -> Void) {
    guard (identifier == "com.example.my-download-session") else { return }
    let sc =
NSURLSessionConfiguration.backgroundSessionConfigurationWithIdentifier(identi
fier)
    sc.sharedContainerIdentifier = "group.com.example.my-app"
    self.session = NSURLSession(configuration: sc,
      delegate: self,
      delegateQueue: NSOperationQueue.mainQueue())
    self.completionHandler = completionHandler
}

func URLSessionDidFinishEventsForBackgroundURLSession(session: NSURLSession){
  let sc = session.configuration
  guard (sc.identifier == "com.example.my-download-session") else { return }
  self.completionHandler!()
  self.session = nil
}

```

Networking - watchOS

- Use background task assertions to protect small tasks

Sharing Secrets | p230

keychain-access-groups entitlement


```swift
// Add an item
SecItemAdd({ kSecAttrAccessGroup: "com.example.your-app-group"}, result:
NULL)
```


Automatic search behavior for query API

- SecItemUpdate
- SecItemDelete
- SecItemCopyMatching

> [2015 706 Security and Your Apps](https://developer.apple.com/videos/play/wwdc2015/706/)