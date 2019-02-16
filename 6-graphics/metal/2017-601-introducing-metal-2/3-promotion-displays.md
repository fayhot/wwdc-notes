
## ProMotion Displays | 3150 | p92


ProMotion 120 PFS


### Opting in to ProMotion

- UIKit animations use ProMotion automatically
- Metal views require opt-in with Info.plist key
  - `<key>CADisableMinimumFrameDuration</key> <true/>`

### Metal Presentation APIs


#### Present immediately


#### Present after minimum duration

`present(drawable, afterMinimumDuration: 1000.0 / 30.0)`


#### Present at specific time


```
let time : CFTimeInterval = projectNextDisplayTime();
present(drawable, atTime: time)
```


```swift
let targetTime = // project when intend to display this drawable

// render your scene into a command buffer for ‘targetTime’
let drawable = metalLayer.nextDrawable()
commandBuffer.present(drawable, atTime: targetTime)
// after a frame or two...


let presentationDelay = drawable.presentedTime - targetTime

 // Examine presentationDelay and adjust future frame timing

```

### Summary

- 120 FPS
- Reduced latency
- Improved framerate consistency
- Reduced stuttering from missed display deadlines
