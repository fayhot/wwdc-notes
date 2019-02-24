
## HEIF — it’s what’s for dinner


Topic|Time|Page
---|---|---
What is HEIF?|
Low-level HEIF file access||p129
High-level HEIF file access|3245|p156
Capturing HEIF files|4045|p191

Demo - Extreme zooming with HEIF | 2430 | 


What the .HEIC?

Payload | Extension UTI
---|---|---
HEVC Image (Writing)|.HEIC|"public.heic"
H.264 Image |.AVCI|“public.avci"
Anything Else|.HEIF|"public.heif"








### Common PhotoKit Workflows

Display

- PHImageManager for UIImage, AVPlayerItem, or PHLivePhoto
- No code changes needed



Backup

- PHAssetResourceManager provides resources in native format


Sharing

- Compatibility vs Features


### Leaving the Garden

```swift
// for images, check the UTI and convert if needed:
PHImageManager.default().requestImageData(for: asset, options: options, resultHandler: { imageData, dataUTI, orientation, info in
guard let dataUTI = dataUTI else { return }
if !UTTypeConformsTo(dataUTI as CFString, kUTTypeJPEG {
// convert the data to a JPEG representation...
}
// for videos use export preset to specify the format
PHImageManager.default().requestExportSession(forVideo: asset, options: options, exportPreset: AVAssetExportPresetHighestQuality, resultHandler: { exportSession, info in

```

