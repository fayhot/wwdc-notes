ui/2018-219-image-and-graphics-best-practices/readme.md

# [2018 219 Image and Graphics Best Practices](https://developer.apple.com/videos/play/wwdc2018/219)



- UIImage and UIImageView
- [Custom drawing with UIKit](2-custom-drawing-with-uikit.md) | 2200| p72
- Advanced CPU and GPU techniques|3030|p97


Memory & CPU are limited resources!


## Image Rendering Pipeline


## Image Buffers

- In-memory representation of an image
- Each element describes color of a single pixel
- Buffer size is proportional to image size

### Image Buffers - The frame buffer


Data Buffers

- Store contents of an image file in memory Metadata describing dimensions of image
- Image itself encoded as JPEG, PNG, or other (usually compressed) form
- Bytes do not directly describe pixels


### Decoding Concerns

- CPU-intensive process
- Retained for repeat rendering
- Persistent large memory allocation
- Proportional to original image size, not view size


Consequences of Excessive Memory Usage
  
- Increased fragmentation
- Poor locality of reference
- System starts compressing memory
- Process termination


```swift 
// Downsampling large images for display at smaller size
func downsample(imageAt imageURL: URL, to pointSize: CGSize, scale: CGFloat) -> UIImage {

    let imageSourceOptions = [kCGImageSourceShouldCache: false] as CFDictionary
    let imageSource = CGImageSourceCreateWithURL(imageURL as CFURL, imageSourceOptions)!
    let maxDimensionInPixels = max(pointSize.width, pointSize.height) * scale
    let downsampleOptions = [   
        kCGImageSourceCreateThumbnailFromImageAlways: true,
        kCGImageSourceShouldCacheImmediately: true,
        kCGImageSourceCreateThumbnailWithTransform: true,
        kCGImageSourceThumbnailMaxPixelSize: maxDimensionInPixels] as CFDictionary

    let downsampledImage =
    CGImageSourceCreateThumbnailAtIndex(imageSource, 0, downsampleOptions)!
    
    return UIImage(cgImage: downsampledImage)
}
```


```swift
// Downsampling large images for display at smaller size

func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath)
-> UICollectionViewCell {

    let cell = collectionView.dequeueReusableCell(withReuseIdentifier: "Cell", for: indexPath) as! MyCollectionViewCell
    cell.layoutIfNeeded() // Ensure imageView is its final size.
 
    let imageViewSize = cell.imageView.bounds.size
    let scale = collectionView.traitCollection.displayScale
    cell.imageView.image = downsample(imageAt: imageURLs[indexPath.item],
        to: imageViewSize, scale: scale)
    
    return cell
 }
```


Decoding in Scrollable Views 

- Prefetching
- Background decoding/downsampling


```swift
// Asynchronously downsampling on a global queue
func collectionView(_ collectionView: UICollectionView,
prefetchItemsAt indexPaths: [IndexPath]) {

    // Asynchronously decode and downsample every image we are about to show
    for indexPath in indexPaths {
        DispatchQueue.global(qos: .userInitiated).async {

            let downsampledImage = downsample(images[indexPath.row])
            DispatchQueue.main.async { self.update(at: indexPath, with: downsampledImage) }
        }
    }
}
```


## Thread Explosion

- More images to decode than available CPUs
- GCD continues creating threads as new work is enqueued
- Each thread gets less time to actually decode images


```swift 
// Avoiding thread explosion when doing asynchronous work
 
let serialQueue = DispatchQueue(label: "Decode queue") 

func collectionView(_ collectionView: UICollectionView,
    prefetchItemsAt indexPaths: [IndexPath]) {
    
    // Asynchronously decode and downsample every image we are about to show
    for indexPath in indexPaths {
        serialQueue.async {
            let downsampledImage = downsample(images[indexPath.row])
            DispatchQueue.main.async { self.update(at: indexPath, with: downsampledImage) }
        }
    }
}
```

## Image Sources

- Image assets in asset catalog
- Files in application/framework bundle
- Files in Documents and Caches directories
- Data downloaded from network


### Prefer Image Assets

- For artwork bundled with your app
- Optimized name- and trait-based lookup Smarter buffer caching
- Per-device thinning
- Vector artwork

## Vector Artwork Optimizations

- Xcode rasterizes artwork for relevant scale factors while compiling
- Prerasterized artwork used when image is drawn at natural size
- If artwork has fixed sizes, use multiple image assets instead of relying on vector rasterization
