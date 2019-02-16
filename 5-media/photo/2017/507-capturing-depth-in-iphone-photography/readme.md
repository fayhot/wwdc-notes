# [2017 507 Capturing Depth in iPhone Photography](https://developer.apple.com/videos/play/wwdc2017/507)


by Brad Ford, Purveyor of Deep Thoughts

507-capturing-depth-in-iphone-photography.md


Topic | Time
--|--
[Depth and disparity on iPhone 7 Plus](1-depth-disparity.md) |
[Streaming depth data from the camera](2-streaming.md) | 2230
[Capturing photos with depth data](3-capturing.md) | 3410
[Dual photo capture](4-dual.md) | 4530


## Depth and disparity on iPhone 7 Plus


## Streaming Depth Data - 2230

### Demo

## Capturing Photos with Depth - 3410

### Demo

## Dual Photo Capture - 4530

### Demo

## Summary - 56

* iPhone 7 Plus Dual Camera is a disparity system
* The canonical representation for depth is AVDepthData
* Intrinsic, extrinsic, and lens distortion info are stored in AVCameraCalibrationData
* Filtered/unfiltered depth is streamed using AVCaptureDepthDataOutput
* Depth is captured in photos using AVCapturePhotoOutput
* Dual Camera Dual Photo Delivery produces wide and tele plus calibration


### Sample Code
* AVCam
* AVCamPhotoFilter
* Wiggle Me
