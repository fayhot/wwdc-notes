## Barcode - David - 3530


Framework Barcode Support

Several frameworks support various barcodes types


### CIBarcodeDescriptor Objects Contain

* The errorCorrectedPayload of the barcode
* Additional code-specific properties such as
  * Aztec’s layerCount
  * QRCode’s maskPattern

```swift
// Get a CIBarcodeDescriptor from AVFoundation.framework
class MyMetadataOutputObjectsDelegate: NSObject, AVCaptureMetadataOutputObjectsDelegate {

func metadataOutput(_ output: AVCaptureMetadataOutput,
  metadataObjects: [AVMetadataObject],
  from connection: AVCaptureConnection) {

    if let mrc = metadataObjects.first as? AVMetadataMachineReadableCodeObject,
      let descriptor = mrc.descriptor {
        print(descriptor)
    }
}
}
```

#### Vision

code

#### CoreImage

code

### Demo: Detection and Re-Generation of a QRCode
