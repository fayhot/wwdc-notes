
## [Filtering with depth data](3-filtering-with-depth-data.md)| - Stephen Ward, Alexandre Naaman - 1536

Topic | Presenter | Time
--|--|--
* Simple Background Effects |
* Custom Depth Effect |
* Depth Blur Effect |
* 3D Effect|



Stephen Ward,


```swift
// Code to Sample the Disparity Map with a Tap
// Apply the filter with the sampleRect from the user’s tap. Don’t forget to clamp!
let minMaxImage = normalizedDisparityImage.clampingToExtent().applyingFilter( "CIAreaMinMaxRed", withInputParameters: [kCIInputExtentKey : CIVector(cgRect:sampleRect)])

// A four-byte buffer to store a single pixel value
var pixel = [UInt8](repeating: 0, count: 4)
// Render the image to a 1x1 rect. Be sure to use a nil color space.
context.render(minMaxImage, toBitmap: &pixel, rowBytes: 4,
bounds: CGRect(x:0, y:0, width:1, height:1), format: kCIFormatRGBA8, colorSpace: nil)
// The max is stored in the green channel. Min is in the red.
let disparity = Float(pixel[1]) / 255.0
```
Using Disparity as a Mask


## Custom Depth Effect - Into Darkness

Raising Disparity to a Power

```swift

// CIColorKernel to dim the image background with disparity
kernel vec4 into_darkness(__sample imageColor, __sample normalizedDisparity, float power) {
// Adjust the fall-off intensity with the power slider
float scaleFactor = pow(normalizedDisparity.r, power);
// Scale the original color by the computed intensity
vec4 result = vec4(imageColor.rgb * scaleFactor, imageColor.a);
return result;
}
```

Swift Code

```swift

// How to apply the color kernel to your image in Swift
let outputImage = kernel.apply(withExtent: image.extent,
arguments: [image, normalizedDisparity, power])

```


### [Using CIDepthBlurEffect - Alexandre Naaman, Technical Lead, Core Image](cidepthblureffect.md) 2630


### [Dolly Zoom](dolly-zoom.md) Stephen Ward, 3625
