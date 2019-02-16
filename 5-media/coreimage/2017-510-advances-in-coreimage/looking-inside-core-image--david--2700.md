
## [Looking Inside Core Image](looking-inside-core-image--david--2700.md) | David | 2700

•Quick Look support and other runtime information



```swift
// load image and apply orientation
var image = CIImage( contentsOf: url
options: [kCIImageApplyOrientationProperty: true])
// downsample by 2x
image = image.applying(CGAffineTransform(scaleX:0.5, y:0.5))
```




### CIImage Quick Look

```swift
// load disparity image and apply orientation
var disparity = CIImage(
contentsOf: url,
options: [kCIImageAuxiliaryDisparity: true,
kCIImageApplyOrientationProperty: true]) // cubic upsample by 2x
disparity = disparity.applyingFilter(“CIBicubicScaleTransform”, withInputParameters: [...])
// adjust disparity mask and blend foreground and background
let mask = disparity.applyingFilter(“CIColorControls", withInputParameters:
  [kCIInputContrastKey: 2.0])
mask = mask.applyingFilter(“CIColorClamp")
```

Diagram

```
kernel _cubicUpsample
  src
  scale=[0.380952 0.380952 0 0]
  coefsLT1=[1.5 -2.5 0 1]
  coefsLT2=[-0.5 2.5 -4 2]
  extent=[-6 -6 1524 2028]

affine
    0  -1  0
    1  0  768
    extent=[0 0 576 768] opaque
affine
    1 0 0
    0 -1 576
    extent=[0 0 768 576] opaque

colormatch
 Linear Gray_to_workingspace
 extent=[0 0 768 576] opaque

IOSurface 0x100e720c0(218) seed:1 Lh alpha_one
 extent=[0 0 768 576] opaque
```

### CIImage Quick Look

```swift

// adjustment for foreground
let fg = image.applyingFilter("CIPhotoEffectFade") // adjustment for background
let bg = image.applyingFilter("CIPhotoEffectNoir")
// combine foreground and background using mask
let output = fg.applyingFilter("CIBlendWithMask", withInputParameters:
  [ kCIInputBackgroundImageKey: bg, kCIInputMaskImageKey: mask])

```

```
colorkernel _blendWithMask
  f=image_0
  b=image_1
  m=image_2
  extent=[0 0 1512 2016]


```

### CIRenderInfo Quick Look

```swift

// render output to an IOSurface
let dest = CIRenderDestination(ioSurface: surface)
let context = self.context
guard
  let task = try? context.startTask(toRender: output, to: dest),
  let info = try? task.waitUntilCompleted()
else {
  // handle render failure
}

```
