
## [Sharing UI](4-sharing-ui.md) | Jacob Farkas | 1955 | p114

You and I are going to share some records


### Demo


### iOS Sharing API

* [`UICloudSharingController`](https://developer.apple.com/reference/uikit/uicloudsharingcontroller)
* [`UICloudSharingControllerDelegate`](https://developer.apple.com/reference/uikit/uicloudsharingcontrollerdelegate)
* [`UIApplicationDelegate`](https://developer.apple.com/reference/uikit/uiapplicationdelegate)

#### UIApplicationDelegate

optional func application(_ application: UIApplication,
userDidAcceptCloudKitShareWith cloudKitShareMetadata: CKShareMetadata)

#### Info.plist

```xml
 <key>CKSharingSupported</key>
 <true/>
```

### macOS Sharing API

[`NSSharingService`](https://developer.apple.com/reference/appkit/nssharingservice)


