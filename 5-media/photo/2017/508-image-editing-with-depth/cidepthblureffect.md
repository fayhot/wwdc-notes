

## [Using CIDepthBlurEffect - Alexandre Naaman, Technical Lead, Core Image](cidepthblureffect.md)


```swift
let mainImage =CIImage(contentsOf: url)


let disparityImage = CIImage(contentsOf: url, options: [kCIImageAuxiliaryDisparity : true])

let filter = CIFilter(name :  "CIDepthBlurEffect", withInputParameters: [kCIInputImageKey: mainImage, kCIInputDisparityImageKey: disparityImage])

var resultImage = filter.outputImage

// For each new user action
filter.setValue (aperture  , forKey: inputAperture")
filter.setValue(mornalizedFocusRect, forKey: "inputFocusRect")

resultImage = filter.outputImage

```

### Use Vision to Specify Points of Faces

### Scaling the Output


### Additional Reminders

Create the CIContext with half-float intermediates

```swift
let ctx = CIContext(options: [kCIContextWorkingFormat : kCIFormatRGBAh])
```

### CIDepthBlurEffect: Custom Disparity Upsample
