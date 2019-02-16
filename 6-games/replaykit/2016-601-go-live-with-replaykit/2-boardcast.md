


## [Broadcast](2-boardcast.md) | Edwin | 1200 | p45

Live Broadcast
Broadcast live to 3rd party broadcast services
Directly from iOS / tvOS device
Provide commentary with mic and camera (iOS)
Content is secure and only accessible to the broadcast service



### Initiating a Broadcast

```swift
func didPressBroadcastButton() {
    RPBroadcastActivityViewController.load { broadcastAVC, error in
        if let broadcastAVC = broadcastAVC {
            broadcastAVC.delegate = self
            self.present(broadcastAVC, animated: true)
        } 
    }
}
```

### Starting a Broadcast


```swift
 
func broadcastActivityViewController(
    _ broadcastAVC: RPBroadcastActivityViewController,    
    didFinishWith broadcastController: RPBroadcastController?,
    error: NSError?) {

    broadcastAVC.dismiss(animated: true) {
        self.startCountDownTimer {
            broadcastController?.startBroadcast { error in
                // broadcast started!
            }
        
        }
    }
}
```

### Indicating a Broadcast

- Animate to indicate activity
- Merge with controls if space constrained
- Required during broadcast
- broadcastController.isBroadcasting

```swift
func updateBroadcastButton() {
     if self.broadcastController?.isBroadcasting == true {
         self.startAnimateIndicator()
     } else {
         self.stopAnimatingIndicator()
    } 
}
```

### Finish Broadcast

```swift
func didPressBroadcastButton() {
    self.broadcastController?.finishBroadcast { error in
        if error == nil {
            // broadcast finished!
            self.updateBroadcastUI()
        } 
    }
}
```

### // Error Handling

```swift
func broadcastActivityViewController(
    _ broadcastActivityViewController: RPBroadcastActivityViewController,
    didFinishWith broadcastController: RPBroadcastController?,
    error: NSError?) {
    
    self.broadcastController = broadcastController
    self.broadcastController?. = self 
}


func broadcastController(
    _ broadcastController: RPBroadcastController,
    didFinishWithError error: NSError?) {
    
    if error != nil {
        // error occurred during broadcast
        self.showErrorMessage(message: error!.localizedDescription)
        // update UI to indicate the broadcast is stopped
        self.updateBroadcastUI()
     }
}
```

### // Application Backgrounding

```swift
func applicationWillResignActive() {
// ReplayKit will automatically pause the broadcast
}
func applicationDidBecomeActive() {
    if self.broadcastController?.isBroadcasting == true {
        self.promptUserToResumeBroadcast { userWantsToResume in
            if (userWantsToResume == true) {
                // user wants to resume
                self.broadcastController?.resumeBroadcast()
                self.updateBroadcastUI()
            } else {
                // user does not want to resume
                self.broadcastController?.finishBroadcast { error in
                    self.updateBroadcastUI()
                }

```


### Classes and Protocols

Game API

- RPBroadcastActivityViewController RPBroadcastController
• Present installed broadcast services
- RPBroadcastActivityViewControllerDelegate
• Notified when broadcast setup is complete
• Start and finish broadcast
• Check if broadcast is in-progress
- RPBroadcastControllerDelegate
• Handle errors during broadcast