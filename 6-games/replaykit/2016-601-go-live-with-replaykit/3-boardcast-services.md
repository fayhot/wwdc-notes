
## [Broadcast Services](3-boardcast-services.md) | | | 



- Broadcast UI Extension
  - Set up broadcast
- Broadcast Upload Extension
  - Process and upload video and audio data

Broadcast Extensions

- Embedded in your application
- Execute alongside other application processes
- Can share data between parent application
- Limited in resources compared to applications

Xcode Templates

- New Target templates available in Xcode
- Add Target -> iOS/tvOS -> Application Extension
- Pre-configured with NSExtension properties in info.plist
- Broadcast UI Extension
- Broadcast Upload



### Broadcast UI Extension

- Authenticate the user and provide sign-up Accept terms and conditions
- Set up the broadcast
- Optionally share via social media
- Notify setup is complete
- Set Up a Broadcast
 



### Broadcast Upload Extension

- Receive and process video and audio data
- Upload to server
- Implementation to be defined by broadcast services Work together with us




Live Broadcasting


Expanded Commentary Options
FaceTime camera support Flexible microphone recording Available in iOS 10


FaceTime Camera Support
RPScreenRecorder.shared().isCameraEnabled
Camera preview view available in RPScreenRecorder Subclass of UIView
Position to not obstruct gameplay
Optionally allow the user to move it


RPScreenRecorder.shared().isCameraEnabled = true
if let cameraPreview = RPScreenRecorder.shared().cameraPreviewView {
    cameraPreview.frame = CGRect(...)
    self.view.addSubview(cameraPreview)
}

Microphone Support

```swift
func enableMic {
    RPScreenRecorder.shared().isMicrophoneEnabled = true
}
func disableMic {
    RPScreenRecorder.shared().isMicrophoneEnabled = false
}
```