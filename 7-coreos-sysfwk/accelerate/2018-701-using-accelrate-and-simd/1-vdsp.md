
## [vDSP](1-vdsp.md) 


Signal Processing Library

- Basic operations on arrays
- Discrete Fourier/Cosine Transform
  - 1D DFT/DCT/FFT 2D FFT
- Convolution and correlation

###  Demo • Extract signal from noise

Sample Code: [Signal Extraction from Noise](https://developer.apple.com/documentation/accelerate/vdsp/discrete_fourier_transforms/signal_extraction_from_noise)

### Slide

Essential Computations

- Analyze noisy signal with forward DCT
- Remove frequency components of amplitude less than threshold
- Reconstruct clean signal with inverse DCT


### Code: 

```swift
// Create a Forward DCT Setup Object for vDSP_DCT_Execute
let dctSetup_FORWARD: vDSP_DFT_Setup = {
    guard let dctSetup = vDSP_DCT_CreateSetup(
        nil, vDSP_Length(numSamples), .II) else {
            fatalError("can't create FORWARD vDSP_DFT_Setup")
    }
    return dctSetup
}()


// Perform Forward DCT
var forwardDCT = [Float](repeating: 0,
count: numSamples)
vDSP_DCT_Execute(
    dctSetup_FORWARD, 
    noisySignalReal, 
    &forwardDCT)


// All Values in `forwardDCT` Less Than `threshold` To 0
vDSP_vthres(forwardDCT, stride, &threshold, &forwardDCT, stride, count)


// Create an Inverse DCT Setup Object for vDSP_DCT_Execute
let dctSetup_INVERSE: vDSP_DFT_Setup = {
    guard let dctSetup = vDSP_DCT_CreateSetup(
    nil, vDSP_Length(numSamples), .III) else {
        fatalError("can't create INVERSE vDSP_DFT_Setup")
    }
    return dctSetup
}()


// Reconstruct Clean Signal
vDSP_DCT_Execute(
    dctSetup_INVERSE, 
    forwardDCT, 
    &inverseDCT)
// Apply Normalization Factor
var divisor = Float(count)
vDSP_vsdiv(
    inverseDCT, 
    stride, 
    &divisor, 
    &inverseDCT, 
    stride, 
    count)

```


## • Demo • Halftone de-screening | 822

Code: [Halftone Descreening with 2D Fast Fourier Transform](https://developer.apple.com/documentation/accelerate/vdsp/fast_fourier_transforms/halftone_descreening_with_2d_fast_fourier_transform)

## Essential Computations

- Transform halftone image with 2D FFT
- Remove frequency components of the halftone screen
- Reconstruct continuous tone image

### // Create a FFT Setup Object, No Direction Specified

```swift 
let fftSetUp: FFTSetup = {
    let log2n = vDSP_Length(log2(1024.0 * 1024.0))
    guard let fftSetUp = vDSP_create_fftsetup(log2n, FFTRadix(kFFTRadix2)) else {
        fatalError("can't create FFT Setup")
    }
    return fftSetUp
}()
```


### // Perform 2d FFT

```swift

let sourceImage_floatPixels_frequency = DSPSplitComplex(
    realp: &sourceImage_floatPixelsReal_spatial,
    imagp: &sourceImage_floatPixelsImag_frequency)

vDSP_fft2d_zrop(fftSetUp, 
    &sourceImageSplitComplex, 
    vDSP_Stride(1), vDSP_Stride(0),
    &sourceImage_floatPixels_frequency, 
    vDSP_Stride(1), 
    vDSP_Stride(0),
    vDSP_Length(log2(Float(width))),
    vDSP_Length(log2(Float(height))),
    FFTDirection(kFFTDirection_Forward))


```


### Frequency Removal

- zvmags 
- vthrsc 
- vclip
- zrvmul


### // Perform Inverse FFT to Create Image from Frequency Domain Data

[`vDSP_fft2d_zrop`](https://developer.apple.com/documentation/accelerate/1450361-vdsp_fft2d_zrop)

```swift 

var floatPixels_spatial = DSPSplitComplex(
    realp: &floatPixelsReal_spatial,
    imagp: &floatPixelsImag_spatial)

vDSP_fft2d_zrop(fftSetUp,
    &sourceImage_floatPixels_frequency,
    stride, 0,
    &floatPixels_spatial,
    stride, 0,
    vDSP_Length(log2(Float(width))), 
    vDSP_Length(log2(Float(height))),
    FFTDirection(kFFTDirection_Inverse))
 
```

