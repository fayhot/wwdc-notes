
## Streaming Depth Data - 2230

### Demo - AVCamPhotoFilter

### Introducing [`AVCaptureDepthDataOutput`](https://developer.apple.com/documentation/avfoundation/avcapturedepthdataoutput)



* Only supported on Dual Camera
* Dual Camera auto-zooms to 2x (zoom is disabled)
* Dual Camera video formats have a supportedDepthDataFormats property
* AVCaptureDevice has new activeDepthDataFormat property

### Supported Depth Resolutions for Streaming


Preset or Active Format | AVCaptureVideoDataOutput | AVCaptureDepthDataOutput
--|--|--
.photo | 1440x1080 @ 30 | 320x240 @ 24 fps <br/>160x120 @ 24 fps
1280x720@3-30 FPS | 1280x720 @ 30 | 320x180 @ 24 fps <br/>160x90 @ 24 fps
.vga640x480 | 640x480 @ 30 | 320x240 @ 24 fps <br/> 160x120 @ 24 fps







### Depth Frame Rate Examples


VideoDataOutput | DepthDataOutput
--|--
1440x1080 @ 24 | 320x240 @ 24 fps
1440x1080 @ 30 | 320x240 @ 15 fps

### Depth Filtering with AVCaptureDepthDataOutput open var

isFilteringEnabled: Bool

### Unsynchronized Data Output (Problem)

### Synchronized Data Output (Solution)


### Streaming Camera Intrinsics

open class AVCaptureConnection : NSObject {
    open var isCameraIntrinsicMatrixDeliveryEnabled: Bool
}

kCMSampleBufferAttachmentKey_CameraIntrinsicMatrix
