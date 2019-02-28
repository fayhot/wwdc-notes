
## [Sharing UI](4-sharing-ui.md) | Jacob Farkas | 1955 | p114

What is shared?

Who is it shared with?

Share URLs



### Demo


### iOS Sharing API - [`UICloudSharingController`](https://developer.apple.com/reference/uikit/uicloudsharingcontroller) | 2520

```swift
// Create a CloudKit share record
let share = CKShare(rootRecord: rootRecord)
share[CKShareTitleKey] = "Shopping List"
share[CKShareThumbnailImageDataKey] = shoppingListThumbnail

// Create a cloud sharing controller
let sharingController = UICloudSharingController(share: share) {
      (controller: UICloudSharingController,
       prepareCompletionHandler : (CKShare?, CKContainer?, NSError?) -> Void) in


    let modifyOp = CKModifyRecordsOperation(recordsToSave: [rootRecord, share],
      recordIDsToDelete: nil)
    modifyOp.modifyRecordsCompletionBlock = { (_, _, error) in
      prepareCompletionHandler(share, ckContainer, error)
    }
    self.container.privateCloudDatabase.add(modifyOp)
}

// Set sharing options
sharingController.availablePermissions = [.publicOnly, .readWrite]
sharingController.popoverPresentationController?.sourceView = myShareButton
sharingController.delegate = self
self.present(sharingController, animated:true, completion:nil)


```

* [`UICloudSharingController`](https://developer.apple.com/reference/uikit/uicloudsharingcontroller)
* [`UICloudSharingControllerDelegate`](https://developer.apple.com/reference/uikit/uicloudsharingcontrollerdelegate)
* [`UIApplicationDelegate`](https://developer.apple.com/reference/uikit/uiapplicationdelegate)



### macOS Sharing API - [`NSSharingService`](https://developer.apple.com/reference/appkit/nssharingservice) | 2700
 

```swift
// Save the share
let itemProvider = NSItemProvider()
itemProvider.registerCloudKitShare { (prepareCompletionHandler :
      (CKShare?, CKContainer?, NSError?) -> Void) in
   // Save the share and root record
}
let sharingService = NSSharingService(named: NSSharingServiceNameCloudSharing)!
sharingService.delegate = self
sharingService.perform(withItems: [itemProvider])


// Define sharing options
func options(for: NSSharingService, share: NSItemProvider)-> NSCloudKitSharingServiceOptions
{
   return [.allowPublic, .allowReadWrite]
}


```


#### UIApplicationDelegate

optional func application(_ application: UIApplication,
userDidAcceptCloudKitShareWith cloudKitShareMetadata: CKShareMetadata)

#### Info.plist

```xml
 <key>CKSharingSupported</key>
 <true/>
```

### CloudKit JS - Web Sharing UI

