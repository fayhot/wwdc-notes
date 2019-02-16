# [2012 511 Core Image Techniques](https://developer.apple.com/videos/play/wwdc2012/511/)

2012-511-core-image-techniques/readme.md


* • Quick Introduction to Core Image
* • A brief overview of what is new in iOS 6
* • How to write a performant real-time camera app
* • How to leverage OpenGL ES and Core Image simultaneously
* • How to use Core Image to enhance your game



Chendi Zhang



Why Was That Slow?
• UIImageView works best with static images
• Avoid creating a CIContext for each render
• Use lower-level APIs for performance-sensitive work

### Attempt 1

### Attempt 2


### Attempt 3

Can We Go Faster?
* Color management
* Leverage YUV image support
* Reduce the render size



## Vintage

Color Transformation


Effect|Filter
--|--
Color transformation|CIColorCube
Vignette|CIVignette
Film scratches|CILightenBlendMode
Add a border|CISourceOverCompositing


###  CIColorCube
• An extremely flexible filter
• Used for a variety of different color effects • Often faster than algorithmic filters
• Supports up to a 64x64x64 cube

CIColorCube
Approximating CISepiaTone



Creating a Real-Time Camera Effects App


Attempt 0
