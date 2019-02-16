## Saving depth data

### Transforming Depth Data

Orientation

Crop

Transform

Native resolution

No color matching

### Transforming Depth Data


CVPixelBuffer AVDepthData

```swift
let renderedDepthBuffer: CVPixelBuffer let originalDepthData: AVDepthData
// Create new AVDepthData object from rendered buffer
let outputDepthData = try originalDepthData.replacingDepthDataMap(with: renderedDepthBuffer)
```

### Writing Depth Data with ImageIO

```swift
// Saving Original Depth Data Using ImageIO
let outputURL : URL // output image file

let outputImage : CGImage // output image

let destination = CGImageDestinationCreateWithURL(outputURL , kUTTypeJPEG, 1, nil)

CGImageDestinationAddImage(destination, outputImage, nil)


// Use AVDepthData to get auxiliary data dictionary
let depthData : AVDepthData // output depth data
var auxDataType : NSString?
let auxData = depthData.dictionaryRepresentation(forAuxiliaryDataType: &auxDataType)

// Add auxiliary data to image destination
CGImageDestinationAddAuxiliaryDataInfo(destination, auxDataType, auxData)

// Write image file
let success = CGImageDestinationFinalize(destination)

```


###  Writing Depth Data with Core Image

```swift
// Write image and depth data to a JPEG file
let context: CIContext
try context.writeJPEGRepresentation(of: image, to: outputURL, colorSpace: outputSpace,
options: [kCIImageRepresentationAVDepthData : depthData])
```

```swift
// Write image and depth image to a JPEG file
let disparityImage: CIImage // output disparity image
try context.writeJPEGRepresentation(of: image, to: outputURL, colorSpace: outputSpace,
options: [kCIImageRepresentationDisparityImage : disparityImage])
```
