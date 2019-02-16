## [New CIRenderDestination API](CIRenderDestination.md) | Tony | 1905

A consistent API to render to different destination types
* IOSurface
* CVPixelBuffer
* Metal Texture
* OpenGL Texture
* Memory buffer

Returns immediately if render fails—with an error

* Allow setting of common properties for the destination
 * Alpha mode behavior
 * Clamping mode behavior
 * Destination colorspace
* And some advanced properties
  * Dithering
  * Blending

Reduces the need for multiple CIContexts

### Performance Benefits

* Existing CIContext APIs for rendering to IOSurface or CVPixelBuffer
  * Return to caller when render is completed
* New CIRenderDestination APIs
  * Return to caller when work is issued
* This allows CPU and GPU work to be pipelined efficiently

---

### p92

```swift
// Clear Then Render Foreground Blended with Background
func renderImagePair (foregroundImage : CIImage,
  backgroundImage : CIImage,
  blend : CIBlendKernel = CIBlendKernel.sourceOver
  toSurface : IOSurface)
{
  let dest = CIRenderDestination(ioSurface: toSurface)
  let ctx = getContext() // don’t create a context each time
  try? ctx.startTask(toClear: dest)
  try? ctx.startTask(toRender: backgroundImage, to: dest)
  dest.blendKernel = blend // use one of 37 built-in blend kernels or create your own
  try? ctx.startTask(toRender: foregroundImage, to: dest).waitUntilCompleted()
}
```

### Rendering to Metal Drawable Textures (p98)

```swift
let ctx = getContext() // don’t create a context each time
let texture = currentDrawable.texture
let dest = CIRenderDestination(texture, commandBuffer: cmdBuffer)
try? ctx.startTask(toRender: image, to: dest)
```
### Diagram (Problem)

### Rendering to Metal Drawable Textures Improved

```swift
let ctx = getContext() // don’t create a context each time

while stillDrawing {
  let dest = CIRenderDestination(
    width: 1024, height: 768,
    pixelFormat: MTLPixelFormat.rgba8Unorm,
    commandBuffer: cmdBuffer) { () -> MTLTexture in
      return currentDrawable.texture
    }
  )
  try? ctx.startTask(toRender: image, to: dest)
}
```

### Diagram (Improved)
