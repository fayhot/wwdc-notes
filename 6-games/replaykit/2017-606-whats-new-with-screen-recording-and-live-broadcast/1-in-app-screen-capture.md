
## [In-App Screen Capture](2017-606-1-in-app-screen-capture.md) - Johnny Trenh [4:45]



* Direct access to audio and video samples
* More control and flexibility
* HD quality
* Minimal power usage
* Privacy safeguards
* Simple API


###

```swift

// Capture API
func startCapture(handler captureHandler: ((CMSampleBuffer, RPSampleBufferType, Error?) -> Void)?, completionHandler: ((Error?) -> Void)? = nil)
func stopCapture(handler: ((Error?) -> Void)? = nil)

```

### // Initiating Capture + Capture Handler Block

```swift

func didPressCaptureButton() {
  let sharedRecorder = RPScreenRecorder.shared()
  sharedRecorder.startCapture(handler: { (cmSampleBuffer, rpSampleType, error) in
    switch rpSampleType {
      case RPSampleBufferTypeVideo:   self.videoInput.appendSampleBuffer(samples)
      case RPSampleBufferTypeAudio:   self.audioInput.appendSampleBuffer(samples)
      case RPSampleBufferTypeMic:     self.micInput.appendSampleBuffer(samples)
      default:    println("sample has no matching type")
    }
  }) { (error) in
    updateCaptureButton(didCompleteError:error)

  }
}
```

## iOS Screen Recording and Broadcast | | 12:10 | p34 


### Handling Interruptions

* In-App Recording can be interrupted by iOS Screen Record and Broadcast
* Recordings will be discarded if interrupted by iOS Screen Record and Broadcast
* Application will get delegate call with appropriate RPError
