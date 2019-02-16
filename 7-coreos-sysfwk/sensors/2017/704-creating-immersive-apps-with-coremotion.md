

# [704 Creating Immersive Apps with Core Motion](https://developer.apple.com/videos/play/wwdc2017/704/)


* Overview
* Authorization
* Historical Accelerometer
* DeviceMotion
* Badger with Attitude


## Motion Interfaces

* CMMotionManager
* CMAltimeter
* CMPedometer
* CMMotionActivityManager
* CMSensorRecorder

## Authorization

## Historical Accelerometer

### App Inspiration - Automotive Performance Tracker

Best practices
* Choose the minimum duration
* Decimate if possible

## DeviceMotion


### Reference Frames

[`CMAttitudeReferenceFrame`](https://developer.apple.com/documentation/coremotion/cmattitudereferenceframe)

* xArbitraryZVertical
* xArbitraryCorrectedZVertical
* xMagneticNorthZVertical
* xTrueNorthZVertical


New in iOS 11

var heading: Double { get } // in CMDeviceMotion

## Badger with Attitude
