
## Depth and disparity on iPhone 7 Plus

Wide-angle lens

Telephoto lengs

### Dual Camera Zoom

* Switches between wide and tele automatically
* Matches exposure, focus, and frame rate
* Compensates for parallax shift to smooth the transition


### Deep Learning

Depth Map

### Disparity (parallax)

### Removing Despair from Disparity


use normalized, rather than pixels, to

### Normalized Disparity

### Disparity vs. Depth

* iPhone 7 Plus Dual Camera system is disparity based
* Disparity is a proxy for depth
* Normalized disparity is the inverse of depth


## New Term: Depth Data

### Introducing [`AVDepthData`](https://developer.apple.com/documentation/avfoundation/avdepthdata)

* The canonical representation of depth on iOS, macOS, and tvOS
* Class in the AVFoundation framework
* Represents depth or disparity maps
* Converts between depth/disparity formats


16 - half float - GPU
32 bit - float - CPU

```swift
public var kCVPixelFormatType_DisparityFloat16: OSType { get } /* 'hdis' */
public var kCVPixelFormatType_DisparityFloat32: OSType { get } /* 'hdis' */
public var kCVPixelFormatType_DepthFloat16: OSType { get } /* 'hdep' */
public var kCVPixelFormatType_DepthFloat32: OSType { get } /* 'fdep' */


@available(iOS 11.0, *)
open class AVDepthData: NSObject {
open var depthDataType: OSType { get }
open var depthDataMap: CVPixelBuffer { get }
open var isDepthDataFiltered: Bool { get }
open var depthDataAccuracy: AVDepthDataAccuracy { get }
}

```

### Holes

Reasons for holes

* occlusions, creepy finger obscuring
* difficulty in finding features.
  * dark out , color is noisy, edge is hard to find.
  * flat white wall with no texture,

Hole-Reporting in AVDepthData


NaN = Invalid depthDataMap value

open var isDepthDataFiltered: Bool { get }


### Calibration Errors

* Optical Image
* Stabilization Gravity
* Focus Coil


### Depth Data Accuracy
```swift
extension AVDepthData {
public enum Accuracy: Int {
case relative
case absolute }
}
```

d^  = d + e
