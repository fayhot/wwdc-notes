

## tvOS | 455




### Demo 


### Start Recording

```swift
func didPressRecordButton() {
    let sharedRecorder = RPScreenRecorder.shared()
    sharedRecorder.startRecording { error in
        if error == nil {
            self.showIndicatorView(text: "Recording")
        }   
    }
}
```


### Excluding UI

```swift
func showIndicatorView(text: String) {
    recordingIndicatorWindow = UIWindow(frame: UIScreen.main().bounds)
    recordingIndicatorWindow?.isHidden = false
    recordingIndicatorWindow?.backgroundColor = UIColor.clear()
    recordingIndicatorWindow?.isUserInteractionEnabled = false
    let indicatorView = IndicatorView(text: text)
    recordingIndicatorWindow?.addSubview(indicatorView)
}

```

### Stop Recording

```swift
func didPressStopButton() {
    sharedRecorder.stopRecording { previewViewController, error in
        self.hideIndicatorView()
        if error == nil {
            self.previewViewController = previewViewController
            self.previewViewController?.previewControllerDelegate = self
        }       
    }
}
```

### Preview Recording

```swift
// RPPreviewViewController
public var mode: RPPreviewViewControllerMode
func didPressPreviewButton() {
    if let preview = previewViewController {
        preview.mode = .preview
        self.present(preview, animated: true)
    }
}
```

### Share Recording

```swift
// RPPreviewViewController
public var mode: RPPreviewViewControllerMode
func didPressShareButton() {
    if let preview = previewViewController {
        preview.mode = .share
        self.present(preview, animated: true)
    }
}
```

### Dismissing Preview UI

```swift
// RPPreviewViewControllerDelegate
func previewControllerDidFinish(_ previewController: RPPreviewViewController) {
    previewController.dismiss(animated: true)
}
```

### Discarding the Recording

- Automatically discarded when new recording starts
  - One recording allowed at a time, per app
- Discard when preview no longer available
  - Use discardRecording()

### ReplayKit on Apple TV

- Record your app video and audio content
  - Microphone reserved by system
- Preview and share the recording
- Same simple API as iOS
- New in tvOS 10

