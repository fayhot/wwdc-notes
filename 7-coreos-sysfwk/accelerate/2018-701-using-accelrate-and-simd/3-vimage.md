
## [vImage](3-vimage.md)  | Luke Chang | 1930 

Image Processing Library

- Conversion
- Geometry
- Convolution
- Transform
- Morphology

### Demo 2230

Sample Code: [Real-Time Video Effects with vImage](https://developer.apple.com/documentation/accelerate/vimage/real-time_video_effects_with_vimage)

### Workflow 

- Receive captured image from camera
- Prepare vImage input/output buffers
- Apply effects with vImage functions
- Display output image on screen


#### Step 3: Adjust Color Saturation

The formula to adjust color saturation is:

```
Cb = ((Cb - 128) * saturation) + 128 
Cr = ((Cr - 128) * saturation) + 128
```

Code

```swift
var preBias: Int16 = -128

// Fixed-Point Arithmetics in Q12 Format
let divisor: Int32 = 0x1000
var postBias: Int32 = 128 * divisor
 
// Convert Saturation to Q12 Format
 var matrix = [ Int16(saturation * Float(divisor)) ]
 
vImageMatrixMultiply_Planar8(
    &sources, 
    &destinations, 1, 1,
    &matrix, divisor, 
    &preBias, &postBias,
    vImage_Flags(kvImageNoFlags))
```

#### Step 1: Receive captured image from camera


```swift 
// AVCaptureVideoDataOutputSampleBufferDelegate
func captureOutput(_ output: AVCaptureOutput,
    didOutput sampleBuffer: CMSampleBuffer,
    from connection: AVCaptureConnection) {

    // Get CVImageBuffer from CMSampleBuffer
    let pixelBuffer = sampleBuffer.imageBuffer
 
    // Make Sure pixelBuffer Is Accessible to CPU
    CVPixelBufferLockBaseAddress(pixelBuffer, .readOnly)
    // Apply Effects with vImage Functions
    ...
 
    // Unlock the BaseAddress of pixelBuffer
    CVPixelBufferUnlockBaseAddress(pixelBuffer, .readOnly)
}
```



#### Step 2: Prepare vImage input/output buffers

[`vImage_Buffer`](https://developer.apple.com/documentation/accelerate/vimage_buffer)

[`vImageBuffer_Init`](https://developer.apple.com/documentation/accelerate/1399064-vimagebuffer_init)

```swift
// Prepare vImage Input Buffer for Luminance
let lumaBaseAddress = CVPixelBufferGetBaseAddressOfPlane(pixelBuffer, 0)
let lumaWidth = CVPixelBufferGetWidthOfPlane(pixelBuffer, 0)
let lumaHeight = CVPixelBufferGetHeightOfPlane(pixelBuffer, 0)
let lumaRowBytes = CVPixelBufferGetBytesPerRowOfPlane(pixelBuffer, 0)
var sourceLumaBuffer = vImage_Buffer(
    data: lumaBaseAddress,
    height: vImagePixelCount(lumaHeight),
    width: vImagePixelCount(lumaWidth),
    rowBytes: lumaRowBytes)

// Prepare vImage Input Buffer for Chrominance
 

```

##### Output Buffer

```swift 
// Initialize vImage Output Buffer
var destinationBuffer = vImage_Buffer()
vImageBuffer_Init(
    &destinationBuffer,
    sourceLumaBuffer.height, 
    sourceLumaBuffer.width,
    cgImageFormat.bitsPerPixel, 
    vImage_Flags(kvImageNoFlags))
```


#### Step 4: Display output image on screen


```swift 
// Convert YCbCr Image to ARGB
vImageConvert_420Yp8_CbCr8ToARGB8888(
    &sourceLumaBuffer, 
    &sourceChromaBuffer,
    &destinationBuffer, 
    &infoYpCbCrToARGB,
    nil, 
    255, 
    vImage_Flags(kvImageNoFlags))

// Create CGImage from vImage_Buffer for Display
// Creating CGImage Object Does Not Copy Image Buffers
let cgImage = vImageCreateCGImageFromBuffer(
    &destinationBuffer, 
    &cgImageFormat,
    nil, 
    nil, 
    vImage_Flags(kvImageNoFlags),
    &error)


// Display the Image on Screen
if let cgImage = cgImage, error == kvImageNoError {
    DispatchQueue.main.async {
        self.imageView.image = UIImage(cgImage: cgImage.takeRetainedValue())
    }
    
}

```

## Other Effects | 2855

- Rotation
- Blur
- Dither
- Color quantization

## Demo • More video effects | 29:25

#### Rotation Effect [`vImageRotate_ARGB8888`](https://developer.apple.com/documentation/accelerate/1509284-vimagerotate_argb8888)



```swift
let backcolor: [UInt8] = [255, 255, 255, 255] 
vImageRotate_ARGB8888(
    &destinationBuffer, 
    &destinationBuffer, 
    nil,
    fxValue, 
    backColor, 
    vImage_Flags(kvImageBackgroundColorFill))

```

#### Blur Effect [`vImageTentConvolve_ARGB8888`](https://developer.apple.com/documentation/accelerate/1515935-vimagetentconvolve_argb8888)

```swift
vImageTentConvolve_ARGB8888(
    &tmpBuffer, &destinationBuffer, nil, 
    0, 0, kernelSize, kernelSize, nil,
    vImage_Flags(kvImageEdgeExtend))
```

#### Dither Effect

```swift
vImageConvert_Planar8toPlanar1(
    &sourceLumaBuffer, 
    &ditheredLuma,
    nil, 
    Int32(kvImageConvert_DitherAtkinson), 
    vImage_Flags(kvImageNoFlags))

```


#### Color Quantization Effect

[`Pixel_8`](https://developer.apple.com/documentation/accelerate/pixel_8) `typealias Pixel_8 = UInt8`

[`vImageTableLookUp_ARGB8888`](https://developer.apple.com/documentation/accelerate/1533201-vimagetablelookup_argb8888)

```swift
var lookUpTable = (0...255).map {
    return Pixel_8(($0 /quantizationLevel) * quantizationLevel)
}
vImageTableLookUp_ARGB8888(
    &destinationBuffer, 
    &destinationBuffer, 
    nil, 
    &lookUpTable, 
    &lookUpTable, 
    &lookUpTable,
    vImage_Flags(kvImageNoFlags))

```
