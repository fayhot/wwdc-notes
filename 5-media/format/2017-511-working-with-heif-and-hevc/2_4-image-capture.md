2_4-capture.md


## Capturing HEIF files|4045|p191





Faster CMSampleBuffer replacement 100% immutable
Backed by containerized data
NEW
 

```swift
open class AVCapturePhoto : NSObject {
    open var timestamp: CMTime { get }
    open var isRawPhoto: Bool { get }
    open var pixelBuffer: CVPixelBuffer? { get }
    open var previewPixelBuffer: CVPixelBuffer? { get }
    open var embeddedThumbnailPhotoFormat: [String : Any]? { get }
    open var metadata: [String : Any] { get } 
    open var depthData: AVDepthData? { get }
    open var resolvedSettings: AVCaptureResolvedPhotoSettings { get }
    open var photoCount: Int { get }
    open var bracketSettings: AVCaptureBracketedStillImageSettings? { get }
    open var sequenceCount: Int { get }
    open var lensStabilizationStatus: AVCaptureDevice.LensStabilizationStatus { get }

    open func fileDataRepresentation() -> Data?

    open func cgImageRepresentation() -> Unmanaged<CGImage>?
    open func previewCGImageRepresentation() -> Unmanaged<CGImage>?
}
```


func photoOutput(_ output: AVCapturePhotoOutput, didFinishProcessingPhoto photo: AVCapturePhoto,
error: Error?)
