

## Grand Central Dispatch
Create a private queue
Schedule asynchronous work items
GCD can automatically wrap each work item in an autorelease pool
 
 
let q = DispatchQueue(label: "com.example.queue", attributes: [.autoreleaseWorkItem])
  Concurrent Programming With GCD in Swift 3
Pacific Heights
Friday 4:00PM


## Foundation

Swift improvements Units and measurements NSISO8601DateFormatter NSDateInterval
 What’s New in Foundation for Swift Measurements and Units
Mission Presidio
Tuesday 4:00PM Friday 4:00PM



UIPasteboard
Universal Clipboard
A paste operation might have to retrieve   remote data
Check for Pasteboard content without fetching


Wide Color
Technology shift
From sRGB to extended sRGB iOS 9.3 is color managed! Exposed as API in iOS 10.0



Image Renderer
UIGraphicsBeginImageContext and UIGraphicsEndImageContext
32 bits and sRGB only Error prone
Not extensible





New UIGraphicsRenderer class
NEW
Fully color managed Block-based
Subclasses for images and PDF
•
•
•
• Manages context lifetime
 
```swift
func createDrawing(size: CGSize) -> UIImage {
    let renderer = UIGraphicsImageRenderer(size: size)
    return renderer.image { rendererContext in

    } 
}

```


Asset Management
Wide color assets Directional image assets Compression
Integrated with the UIKit trait system
NEW
