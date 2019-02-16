## Adjusting RAW Images with Core Image - 750


### Demo : RawExpose - 1330


### CIRAWFilter - 1700

```swift
// Using the CIRAWFilter API
func getAdjustedRAW(url: URL) -> CIImage?
{
    // Load the image
    let f = CIFilter(imageURL: url, options:nil)
    // Get the NR amount
    if let nr = f.value(forKey: kCIInputLuminanceNoiseReductionAmountKey) {
        // Change the NR amount
        f.setValue(nr.doubleValue + 0.1,
                   forKey: kCIInputLuminanceNoiseReductionAmountKey)
}
    // Get the adjusted image
    return f.outputImage
}
```

x


### // Saving a RAW to a JPEG or TIFF

```swift
func save(from rawImage: CIImage,
          to jpegDestination: URL) throws
{
    let cs = CGColorSpace(name: CGColorSpace.displayP3)!
    try contextForSaving.writeJPEGRepresentation(
            of: rawImage,
            to: jpegDestination,
            colorSpace: cs,
            options: [kCGImageDestinationLossyCompressionQuality: 1.0,
            kCGImageDestinationOptimizeColorForSharing: true
            ])
}

```


### // Saving a RAW to a CGImageRef

```swift
func createCGImage(from rawImage: CIImage) -> CGImage?
{
   return contextForSaving.createCGImage(
        rawImage,
        from: rawImage.extent,
        format: kCIFormatRGBAh,
        colorSpace: CGColorSpace(name: CGColorSpace.extendedLinearSRGB),
        deferred: true) // process the RAW when returned CGImage is drawn
}
```



### Supporting wide gamut

* CIKernel Language uses float precision
  * When needed, intermediate buffers use the CIContext’s current working format
  * On macOS, the default working format is kCIFormatRGBAh
  * On iOS/tvOS, the default working format is kCIFormatBGRA8
  * RAW pipeline CIKernels always use kCIFormatRGBAh working format
* Create your CIContext with a kCIContextWorkingFormat option  set to kCIFormatRGBAh ensure wide gamut won’t be clipped.
* Core Image supports wide gamut output color spaces

Warning:“Objects are larger than they appear”
