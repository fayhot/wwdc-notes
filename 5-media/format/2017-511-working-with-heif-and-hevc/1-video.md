
# Video


Topic|Time|Page
---|---|---
Access|  215
Playback | 315
Capture|619
[Export](1_4-video-export.md)|1000|p49



Decode Capability

- Useful for non-realtime operations
- Can be limited by hardware support
- assetTrack.isDecodable


Playback Capability

- Not all content can be played back in realtime
- Differing capabilities on device
- assetTrack.isPlayable

Hardware Decode Availability

- Longest battery life
- Best decode performance
- let hardwareDecodeSupported = VTIsHardwareDecodeSupported(kCMVideoCodecType_HEVC)



```swift
let session = AVCaptureSession() session.sessionPreset = .hd4K3840x2160
let camera = AVCaptureDevice.default(.builtInWideAngleCamera, for: nil, position: .back) let input = try! AVCaptureDeviceInput(device: camera!)
session.addInput(input)
let movieFileOutput = AVCaptureMovieFileOutput() session.addOutput(movieFileOutput)
session.startRunning()
movieFileOutput.startRecording(to: url, recordingDelegate: self)


```

```swift
let connection = movieFileOutput.connection(with: .video)
if movieFileOutput.availableVideoCodecTypes.contains(.hevc) {
outputSetings = [AVVideoCodecKey: AVVideoCodecType.hevc] } else {
outputSetings = [AVVideoCodecKey: AVVideoCodecType.h264] }
movieFileOutput.setOutputSettings(outputSetings, for: connection!)
```


### Capturing Live Photo Movies with HEVC


- Video stabilization
- Music playback
- 30 FPS


```swift
let photoSettings = AVCapturePhotoSettings() photoSettings.livePhotoMovieFileURL = URL(fileURLWithPath: myFilePath) if photoOutput.availableLivePhotoVideoCodecTypes.contains(.hevc) {
photoSettings.livePhotoVideoCodecType = .hevc }
photoOutput.capturePhoto(with: photoSettings, delegate: self)

```


### Capturing HEVC Movies with AVAssetWriter

- Configure AVAssetWriterInput with output settings
- Video data output can recommend settings

```swift
// iOS 7
vdo.recommendedVideoSettingsForAssetWriter(writingTo: .mov)
// iOS 11
vdo.recommendedVideoSettings(forVideoCodecType: .hevc, assetWriterOutputFileType: .mov)
```
