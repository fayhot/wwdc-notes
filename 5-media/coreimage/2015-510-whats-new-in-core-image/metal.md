
## Core Image and Metal - Tony - 1405

```swift
override func viewDidLoad()
{
    super.viewDidLoad()
    // setup view properties
    let view = self.view as! MTKView
    view.delegate = self
    view.framebufferOnly = false
    context = CIContext(MTLDevice: device)
}
```

```swift
func drawInView(view: MTKView)
{
    let commandBuffer = commandQueue.commandBuffer()
    var image = CIImage(MTLTexture: srcTexture!, options: nil)
    image = image.imageByApplyingFilter(“CIGaussianBlur”,
        withInputParameters: [kCIInputRadiusKey: 50])
    let outputTexture = view.currentDrawable?.texture
    context.render(image, toMTLTexture: outputTexture!,
        commandBuffer: commandBuffer, bounds: image.extent, colorSpace: cs)
    commandBuffer.presentDrawable(view.currentDrawable!)
    commandBuffer.commit()
}

```


### AVFoundation


```swift
let vidComp = AVVideoComposition(asset: avAsset,
    applyingCIFiltersWithHandler: {
request in
        let seconds = CMTimeGetSeconds(request.compositionTime)
        let filtered = request.sourceImage.imageByApplyingFilter("OldeFilm",
               withInputParameters: [kCIInputTimeKey: seconds])
        request.finishWithImage(filtered, context: nil)
   })
```

#### // Creating a filtered composition without color management

```swift
let cicontext = CIContext(options: [kCIContextWorkingColorSpace: NSNull()])
let vidComp = AVVideoComposition(asset: avAsset,
    applyingCIFiltersWithHandler: {
        request in
        let seconds = CMTimeGetSeconds(request.compositionTime)
        let filtered = request.sourceImage.imageByApplyingFilter("OldeFilm",
               withInputParameters: [kCIInputTimeKey: seconds])
        request.finishWithImage(filtered, context: cicontext)
   }
)
```


#### Convolution filters with clamped edges

```swift
let vidComp = AVVideoComposition(asset: avAsset,
    applyingCIFiltersWithHandler: {
        request in
        filtered = request.sourceImage.imageByClampingToExtent();
        filtered = filtered.imageByApplyingFilter("CIGaussianBlur",
                      withInputParameters: [kCIInputRadiusKey: 100])
        filtered = filtered.imageByCroppingToRect(request.sourceImage.extent)
        request.finishWithImage(filtered, context: cicontext)
   })
```
