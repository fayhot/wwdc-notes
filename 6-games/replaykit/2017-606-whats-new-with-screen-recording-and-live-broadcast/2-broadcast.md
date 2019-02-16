
## [Live Broadcast](2017-606-2-broadcast.md) - Alexander Subbotin [16:36]

* Broadcast app visuals and audio
* iOS and tvOS
* Can include microphone, camera feed
* Content is secure


[RPBroadcastActivityViewController]()


## Live Broadcast - App extensions [20:20]

[RPScreenRecorder](https://developer.apple.com/documentation/replaykit/rpscreenrecorder)



Broadcast SetupUI Extension

* UI to login, get broadcast name and other
* Uploads name and icon of the app
* Provides broadcast URL back to client app
* NSExtensionContext(RPBroadcastExtension)
  * loadBroadcastingApplicationInfo
  * completeRequest(withBroadcast)


```swift
// Get name and icon for client application and provide to the broadcast service
class BroadcastSetupViewController: UIViewController { override func viewDidLoad() {
super.viewDidLoad() extensionContext?.loadBroadcastingApplicationInfo(completion: {
(bundleID, displayName, appIcon) in broadcastSession.setAppInfo(bundleID, displayName, appIcon)
}) }
}
```

## Broadcast Upload Extension

* Receives audio and video samples
* Encodes and uploads stream to broadcaster

```swift
// SampleHandler created by Xcode templates for Upload Extension
class SampleHandler: RPBroadcastSampleHandler {
override func broadcastStarted(withSetupInfo setupInfo: [String : NSObject]?) {
// User has requested to start the broadcast
}
override func broadcastPaused() {
// User has requested to pause the broadcast. Samples will stop being delivered.
}
override func broadcastResumed() {
// User has requested to resume the broadcast. Samples delivery will resume.
}
override func broadcastFinished() {
// User has requested to finish the broadcast
}
override func processSampleBuffer(_ sampleBuffer: CMSampleBuffer,
with sampleBufferType: RPSampleBufferType) {
// Handle the sample buffer here
}
}
```

```swift
// Both audio and video samples are handled by processSampleBuffer routine
override func processSampleBuffer(_ sampleBuffer: CMSampleBuffer,
with sampleBufferType: RPSampleBufferType) {
switch sampleBufferType {
case RPSampleBufferType.video:
var imageBuffer:CVImageBuffer = CMSampleBufferGetImageBuffer(sampleBuffer)! var pts = CMSampleBufferGetPresentationTimeStamp(sampleBuffer) as CMTime VTCompressionSessionEncodeFrame(session, imageBuffer, pts,
kCMTimeInvalid, nil, nil, nil)
break
case RPSampleBufferType.audioApp:
// Handle audio sample buffer for app audio
break
case RPSampleBufferType.audioMic:
} }
```
