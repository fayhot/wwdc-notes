## [Framework updates](1-framework-updates.md)


Performance

- Scrolling | | p6
- Memory | 1115 | p26
- Auto Layout | 1730 | p39



```swift
// UITableView Cell Load Cost
import UIKit
class MyTableViewDataSource {
    func tableView(_ tableView: UITableView,
    cellForRowAt indexPath: IndexPath) -> UITableViewCell {

        // Dequeue or allocate cell
        // Populate cell with model data

        return myCell
    }
}

// call layoutSubviews on UIViews in the cell
// call draw() on UIViews in the cell

```

### Memory Is Performance



### Automatic Backing Store (iOS 12)

- 375w x 250h x @3x x 64 bpp = 2.2 megabytes
- 375w x 250h x @3x x 8 bpp = 275 kilobytes

x

- Automatic is now default
  - UIView.draw()
  - UIGraphicsImageRenderer
  - UIGraphicsImageRendererFormat.Range
 
> [2018 219 Image and Graphics Best Practices](https://developer.apple.com/videos/play/wwdc2018/219)


### Auto Layout | 1730 | p39



### Swiftification 

Nesting

- Types
- Constants
- Functions


// Nested Constants

```swift
// Swift 4
class NSNotification : NSObject {
    struct Name {
        class let didChangeStatusBarOrientation: NSNotification.Name
    }
    
}
let UIApplicationStatusBarOrientationUserInfoKey: String

// Swift 4.2
class UIApplication : UIResponder {
    class let didChangeStatusBarOrientationNotification: NSNotification.Name
    class let statusBarOrientationUserInfoKey: String
}
```

// Nested Functions — String Conversion

```swift
// Swift 4
NSStringFrom[CGPoint, CGRect, CGSize, CGVector, CGAffineTransform, UIEdgeInsets, UIOffset]
[CGPoint, CGRect, CGSize, CGVector, CGAffineTransform, UIEdgeInsets, UIOffset]FromString
// Swift 4.2 – Codable Conformance
let encoded = JSONEncoder().encode(CGPoint(x: 0, y: 0))
let decoded = JSONDecoder().decode(CGPoint.self, from: encoded)


// Swift 4.2 — Debug Printing
print(CGPoint(x: 0, y: 0))
print(“Offset: \(UIOffset(horizontal: 10, vertical: 10))”)

// Swift 4.2 — Legacy Encoding/Decoding
let encoded = NSCoder.string(for: CGPoint(x: 0, y: 0))
let decoded = NSCoder.cgPoint(for: encoded)

```

NSSecureCoding

- New secure-by-default encoding and decoding APIs
- Older APIs now deprecated

[2018 222 Data You Can Trust](https://developer.apple.com/videos/play/wwdc2018/222)