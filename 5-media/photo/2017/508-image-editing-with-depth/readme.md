
# [2017 508 Image Editing with Depth](https://developer.apple.com/videos/play/wwdc2017/508/)

Etienne Guerard 　Image Editor-in-Chief

No|Topic|Presenter|Time
--|--|--|--
1| What is depth? |Etienne Guerard| 100
2|Loading depth data | Etienne Guerard| 720
3|[Filtering with depth data](3-filtering-with-depth-data.md)|Stephen Ward, Alexandre Naaman| 1536
4|[Saving depth data](4-save-depth-data.md)| Etienne Guerard| 4300


## What is depth?

iPhone 7 Plus / iOS 11 / Dual camera system / Disparity

## How

2017-508-image-editing-with-depth.md

## Demo: Depth Explorer - Craig Milito - 240


## Effects

Blur background.


### Who can use depth ?

Editing app, Camera app, Sharing app.

## Loading depth data | 720

PHContentEditingInput

PHImageManager


### Testing for Depth Data with ImageIO

### Reading Depth Data


Auxiliary data

AVDepthData

CVPixelBuffer

Single channel Depth or disparity

16-bit or 32-bit float


```swift
// Reading depth data from an image source import ImageIO
let fileURL: URL

let source =  CGImageSourceCreateWithURL   (fileURL,  nil )

// Read auxiliary data of type disparity
let auxDataType = kCGImageAuxiliaryDataTypeDisparity
let auxDataInfo = CGImageSourceCopyAuxiliaryDataInfoAtIndex(source, 0, auxDataType)

 if
}
```


## 3 [Filtering with depth data](3-filtering-with-depth-data.md) - 1536

## 4 [Saving depth data](4-save-depth-data.md) - 4300
