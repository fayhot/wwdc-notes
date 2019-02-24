## [Export](1_4-video-export.md)|1000|p49



Export

Transcode to HEVC with AVFoundation and VideoToolbox
MPEG-4, QuickTime file format container support API opt-in required


### Transcode with AVAssetExportSession


### Export Session

- No change in behavior for existing presets
- Convert from H.264 to HEVC with new presets 
- Produce smaller AVAssets with same quality

```swift
AVAssetExportPresetHEVC1920x1080 AVAssetExportPresetHEVC3840x2160 AVAssetExportPresetHEVCHighestQuality
```

Asset Writer

Specify HEVC with output settings for AVAssetWriterInput

```swift
settings = [AVVideoCodecKey: AVVideoCodecType.hevc]
```

Convenient output settings with AVOutputSettingsAssistant

```swift
AVOutputSettingsPreset.hevc1920x1080 AVOutputSettingsPreset.hevc3840x2160
```


### Valid Output Settings

Query encoder for supported properties in output settings

```swift
let error = VTCopySupportedPropertyDictionaryForEncoder( 3840, 2160,
kCMVideoCodecType_HEVC, encoderSpecification, &encoderID, &properties)
if error == kVTCouldNotFindVideoEncoderErr { // no HEVC encoder
}
```

- Encoder ID is a unique identifier for an encoder
- Properties and encoder ID can be used in output settings

### Compression Session

Create session with HEVC encoder


```swift
let error = VTCompressionSessionCreate( kCFAllocatorDefault,
3840, 2160,
kCMVideoCodecType_H264,
encoderSpecification,
nil, nil, nil, nil, // using VTCompressionSessionEncodeFrameWithOutputHandler &session);
if error == kVTCouldNotFindVideoEncoderErr { // no H.264 encoder
}
```


## Hierarchical Frame Encoding

### Video Encoding 101


