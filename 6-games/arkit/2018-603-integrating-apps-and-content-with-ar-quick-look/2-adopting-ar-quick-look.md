# [Adopting AR Quick Look](2-adopting-ar-quick-look.md)|1020|p11


## Adopting AR Quick Look


### Quick Look

- Preview documents
- Framework for previewing file formats
- Control over transitions and presentation modes
- Secure and private

See [2018 Quick Look Previews from the Ground Up]


### Quick Look Preview Flow

QLPreviewController

### Previewing ‘usdz’ Objects Using Quick Look

QLPreviewController

```swift 
func preview(_ sender: Any) {
    let previewController = QLPreviewController() 
    previewController.dataSource = self 
    previewController.delegate = self
 
    // Present viewer modally
    present(previewController, animated: true, completion: nil)
}
```

QLPreviewControllerDataSource

```swift 
 
func numberOfPreviewItems(in controller: QLPreviewController) -> Int { // Viewer supports previewing a single 3D object
    return 1
}
 
func previewController( _ controller: QLPreviewController, previewItemAt index: Int) -> QLPreviewItem {
// Return the file URL to the .usdz file
 
    let fileUrl = Bundle.main.url(forResource: “radar_aardvark”, withExtension: “usdz”)! 
    return fileUrl as QLPreviewItem
}
```

QLPreviewControllerDelegate


```swift
func previewController(_ controller: QLPreviewController, transitionViewFor item: QLPreviewItem) -> UIView? {
    // Provide the starting view for a seamless zoom transition to the viewer
    return self.startingZoomView
}
```

### Previewing ‘usdz’ Content in Safari

Recommended image-based experience

- HTML markup
- Automatic badging
- Provide custom thumbnail image
- Supports drag and drop
- Supports long-press
- Better workflow

http://mygardenstore.com/ WateringCan.usdz

### HTML Markup for Previewing ‘usdz’ Objects

`<img>` element

```html
<a rel="ar" href="model.usdz"> 
    <img src="model-preview.jpg">
</a>
```

`<picture>` element

```html
<a rel="ar" href="model.usdz">
    <picture>
        <source srcset=“wide-image.png” media="(min-width: 600px)">
        <img src="narrow-image.png">
    </picture>
</a>
```

MIME type

```
AddType model/vnd.pixar.usd .usdz
AddType model/usd usdz
```