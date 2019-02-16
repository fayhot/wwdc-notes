## [Developing Broadcast Extensions](3-developing-broadcast-extensions.md) | 1355 | p39

For ReplayKit 2




Broadcast App and Extension
Broadcast Application
Account sign-in, broadcast title
Broadcast Upload Extension
Encode samples, upload to service
Upload extension
 •
Audio and video  samples
Media stream
  
### Broadcast Upload Extension

- Receives audio and video samples
- Encodes and uploads video stream
- Handles device orientation changes
- Annotates broadcast with app information

Broadcast Extension Template

```swift
// SampleHandler created by Xcode templates for Upload Extension
class SampleHandler: RPBroadcastSampleHandler {
// User has requested to start the broadcast
override func broadcastStarted(withSetupInfo setupInfo: [String : NSObject]?)
// User has requested to finish the broadcast
override func broadcastFinished()
// Handle the sample buffer here
override func processSampleBuffer(_ sampleBuffer: CMSampleBuffer,
with sampleBufferType: RPSampleBufferType)
// Use details of application to annotate the broadcast
override func broadcastAnnotated(withApplicationInfo info: [String : NSObject])
}
```

### Broadcast Lifecycle

### Handling Sign-In and Broadcast Setup

Broadcast application

### Initialization

```swift
// Override init to read login credentials from shared keychain
class SampleHandler : RPBroadcastSampleHandler {
    override func init() {
        super.init()
        session = BroadcastSession.instance
        var credentials = KeychainAccess.getLoginCredentials()
session.authentificate(credentials)
    }
}
```

### Handling broadcastStarted

```swift
// Override broadcastStarted to prepare to receive media samples
override func broadcastStarted(withSetupInfo setupInfo: [String : NSObject]?) {
    // Verify user is logged in
    if (session.userLoggedIn()) {
        session.createMediaEngine()
    }
}
```

### Processing Media Samples

Broadcast Upload Extension
processSampleBuffer

```swift
// Both audio and video samples are handled by processSampleBuffer routine
override func processSampleBuffer(_ sampleBuffer: CMSampleBuffer,
    with sampleBufferType: RPSampleBufferType) {
    
    switch sampleBufferType {
    case RPSampleBufferType.video:
        var imageBuffer:CVImageBuffer = CMSampleBufferGetImageBuffer(sampleBuffer)!
        var pts = CMSampleBufferGetPresentationTimeStamp(sampleBuffer) as CMTime
        VTCompressionSessionEncodeFrame(session, imageBuffer, pts,
            kCMTimeInvalid, nil, nil, nil)
        break
    case RPSampleBufferType.audioApp:
        // Handle audio sample buffer for app audio
        break
    case RPSampleBufferType.audioMic:
        // Handle audio sample buffer for mic audio
        break
    }
}
```

### Handling Application Information

### Broadcast Upload Extension
broadcastAnnotatedWithApplicationInfo

```swift
// Use application details to help users find your broadcast
override func broadcastAnnotated(withApplicationInfo applicationInfo: [AnyHashable : Any]) {
    var bundleIdentifier = applicationInfo[RPApplicationInfoBundleIdentifierKey]
    if (bundleIdentifier != nil) {
        session.addMetadataWithApplicationInfo(bundleIdentifier)
    }
}
```

### Handling broadcastFinished

### Handling Sign-In

```swift
// Override broadcastStarted to prepare to receive media samples
override func broadcastStarted(withSetupInfo setupInfo: [String : NSObject]?) {
    // Verify user is logged in and there’s network connectivity
    if (session.userLoggedIn()) {
        session.createMediaEngine()
    } else {
        let userInfo = [NSLocalizedFailureReasonErrorKey : "Not Logged In"]
        let error = NSError(domain: "RPBroadcastErrorDomain", code: 401, userInfo: userInfo)
        finishBroadcastWithError(error)
    }
}
```


Developing Broadcast Extensions
Summary

- Implement sign-in and setup UI in your application
- Finish the broadcast and send user to the app if something is missing
- Encode and upload video stream to your service
- Use information about app on the screen to help users find your broadcast
