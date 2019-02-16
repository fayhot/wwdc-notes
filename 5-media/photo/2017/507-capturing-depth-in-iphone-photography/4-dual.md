
## Dual Photo Capture - 4530


### Requesting Dual Photo Delivery

Before starting the capture session, opt in!

photoOutput.isDualCameraDualPhotoDeliveryEnabled = true Request Dual

Photo capture on a per-request basis

photoSettings.isDualCameraDualPhotoDeliveryEnabled = true

Number of AVCapturePhoto callbacks doubles

let sourceDeviceType = photo.sourceDeviceType

### Dual Photo Capture

Supports

* Flash captures
* Auto still image stabilization
* Auto exposure brackets
* Depth delivery


### Introducing [`AVCameraCalibrationData`](https://developer.apple.com/documentation/avfoundation/avcameracalibrationdata)


* Property of AVDepthData
* Property of AVCapturePhoto (if you opt in):
  * `photoSettings.isCameraCalibrationDeliveryEnabled = true`



Tele camera is the world origin

open var lensDistortionCenter: CGPoint { get }

open var inverseLensDistortionLookupTable: Data { get }

### Demo - StraightUp (4th and final)
