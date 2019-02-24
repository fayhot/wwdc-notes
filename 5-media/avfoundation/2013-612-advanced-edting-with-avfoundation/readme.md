2013-612-advanced-edting-with-avfoundation/readme.md


# [2013 612 Advanced Editing with AV Foundation](https://developer.apple.com/videos/play/wwdc2013/612/)


- Custom video compositing
  - Existing architecture
  - New custom video compositing
  - Choosing pixel formats
  - Tweening
  - Performance
- Debugging compositions
  - Common pitfalls



## Existing Architecture - AV Foundation editing today
- Available since iOS 4.0 and OS X Lion
- Used in video editing apps from Apple and in the store
- Video editing
  - Temporal composition 
  - Video composition
  - Audio mixing

Possible Today (iOS 7)

- Wipes, Dissolves, Transforms,...

## Custom Video Compositor | 230 | 




### What Is a Video Compositor?

- Unit of video mixing code
- Receives multiple source frames
- Blends or transforms pixels
- Delivers single output frame
- Part of the composition architecture







Composition Model

Video Instructions

Video Compositor

Custom Video Compositor | 520?


[`AVVideoCompositing`](https://developer.apple.com/documentation/avfoundation/avvideocompositing)




Choosing Pixel Formats

Source Pixel Format YUV 8-bit 4:2:0

https://developer.apple.com/documentation/avfoundation/avvideocompositing/1388610-sourcepixelbufferattributes

```swift
var sourcePixelBufferAttributes: [String : Any]? { get }
```

var requiredPixelBufferAttributesForRenderContext: [String : Any] { get }

Demo | 830  - 1450 | p82

Slide - Tweening | 1455



## Performance | 1700

[`AVVideoCompositionInstruction`](https://developer.apple.com/documentation/avfoundation/avvideocompositioninstruction)


var passthroughTrackID: CMPersistentTrackID { get }




## Debugging | 2135 


## Demo | 2350

