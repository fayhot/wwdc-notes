
## Image Picker Improvements - Hasan Adil

 [UIImagePickerController](https://developer.apple.com/documentation/uikit/uiimagepickercontroller)

Obtaining Metadata

* Created Date
* Format of the photo
* Metadata

```swift
// protocol implementation
public func imagePickerController(_ picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [String : Any]) {
if let imageURL = info[UIImagePickerControllerImageURL] as? URL {
}
```

### Accessing New Formats

```swift
var imageExportPreset: UIImagePickerControllerImportExportPreset { get set }

let imagePicker = UIImagePickerController()
imagePicker.imageExportPreset = .compatible
self.present(imagePicker, animated: true, completion: nil)

let imagePicker = UIImagePickerController() 
imagePicker.imageExportPreset = .current
self.present(imagePicker, animated: true, completion: nil)
```


### Getting Videos

```swift
var videoExportPreset: String { get set }

import AVFoundation

let imagePicker = UIImagePickerController()
imagePicker.videoExportPreset = AVAssetExportPresetHighestQuality
self.present(imagePicker, animated: true, completion: nil)
// See AVAssetExportSession
```

### Saving Photos and Videos

```swift
public func UIImageWriteToSavedPhotosAlbum(_ image: UIImage,
  _ completionTarget: Any?, _ completionSelector: Selector?,
  _ contextInfo: UnsafeMutableRawPointer?)

public func UISaveVideoAtPathToSavedPhotosAlbum(_ videoPath: String,
  _ completionTarget: Any?, _ completionSelector: Selector?,
  _ contextInfo: UnsafeMutableRawPointer?)
```


### Getting a PHAsset

* Support for PhotoKit clients
* Easy way to get the PHAsset object

```swift
public func imagePickerController(_ picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [String : Any]) {
  if let asset  = info[UIImagePickerControllerPHAsset] as? PHAsset {
    print(asset)
  }
}

```
