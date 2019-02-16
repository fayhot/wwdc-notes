
## Capturing Photos with Depth - 3410


AVCam

Wiggle Me

Photos with Depth

* Flash
* Auto still image stabilization
* Auto exposure brackets
* Live photos

### High Res Photo Depth Maps

Table

### Rectilinear vs. Lens Distorted Images


### Depth Map Distortions

* Depth data maps work well for applying effects to the images
* Don't work well for 3D-scene reconstruction
* Maps and images can be made rectilinear

### Depth in Image Files


HEIF HEVC (HEIC)

* Map is an auxiliary image
* Encoded as monochrome HEVC
* Metadata is XMP in the auxiliary image



JPEG

* Map is 8-bit lossy JPEG (filtered) or 16-bit lossless (unfiltered) MPO
* Metadata is XMP in the second image
