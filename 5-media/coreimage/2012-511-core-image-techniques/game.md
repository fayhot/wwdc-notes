## Game + Core Image


## Core Image Techniques for Games

Common use cases

* Apply an effect to the full screen
* Apply an effect to individual textures


### Apply an effect to the full screen




### Apply an effect to individual textures


How Did We Do This?
The workflow

1. Create a CIImage, using the texture
2. Create the CIFilter
  ■ Set the kCIInputImageKey value to the CIImage
3. Create an OpenGL texture FBO
  ■ This is the new texture
4. Create a CIContext to filter to
  ■ Targets the new texture
  
