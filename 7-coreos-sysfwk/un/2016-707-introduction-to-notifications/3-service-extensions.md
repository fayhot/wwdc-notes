
## [Service Extensions](3-service-extensions.md) [31]

Non UI iOS Extension

### Potential uses

End-to-end encryption / add attachments

Service Extension . Xcode

[`UINotificationServiceExtension`](https://developer.apple.com/reference/usernotifications/unnotificationserviceextension)



```swift
class NotifSvc : UINotificationServiceExtension {

  override func didReceive(_ request: UNNotificationRequest,
  withContentHandler contentHandler: @escaping (UNNotificationContent) -> Void) {

  }

}
```

### Example payload

```json
{
  aps: {
    mutable-content : 1 
  },

  encrypted-content: “”
}
```