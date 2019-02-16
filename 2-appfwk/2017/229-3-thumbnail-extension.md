

## [Thumbnail Extension](229-3-thumbnail-extension.md) p115 43:30 Maxime Uzan

### Providing Thumbnails: Through UIDocument

* Return the thumbnail from your subclass of UIDocument
* Only for files created by your application
* Good performance, file is already loaded when setting the thumbnail

```swift
override func fileAttributesToWrite(to url: URL, for saveOperation: UIDocumentSaveOperation) throws -> [AnyHashable : Any] {

  let thumbnail = thumbnailForDocument(at: url)
  return [
URLResourceKey.hasHiddenExtensionKey: true, URLResourceKey.thumbnailDictionaryKey: [
    URLThumbnailDictionaryItem.NSThumbnail1024x1024SizeKey: thumbnail ]
  ]
}
```

### Providing Thumbnails: Thumbnail Extension

* System-wide
* Works with all cloud vendors
* Part of the QuickLook framework


### Thumbnail Extension

Getting started—Info.plist

* Add all supported UTIs to the QLSupportedContentTypes array
  * You can only provide thumbnails for UTIs you own and export
  * iOS will check for strict UTI equality, not conformance

### Drawing thumbnails

```swift

override func provideThumbnail(for request: QLFileThumbnailRequest,
_ handler: @escaping (QLThumbnailReply?, Error?) -> Void) {

  let fileURL = request.fileURL
  let maximumSize = request.maximumSize
  let scale = request.scale
  let contextSize = contextSizeForFile(at: fileURL, maximumSize: maximumSize, scale: scale)

  let drawingBlock: (CGContext) -> Bool = { context in
    let  success = self.drawThumbnailForFile(at: fileURL, contextSize: contextSize, context: context)
    return success
  }



  let reply = QLThumbnailReply(contextSize: contextSize, drawing: drawingBlock)
  handler(reply, nil)
}
```

### Image file URL

```swift
override func provideThumbnail(for request: QLFileThumbnailRequest,
_ handler: @escaping (QLThumbnailReply?, Error?) -> Void) {

  if let imageFileURL = Bundle.main.url(forResource: "image", withExtension: "jpg") {   
    handler(QLThumbnailReply(imageFileURL: imageFileURL), nil)
  } else {
    handler(nil, nil)
  }
}

```

### API

* [`QLFileThumbnailRequest`](https://developer.apple.com/documentation/quicklook/qlfilethumbnailrequest)
* [`QLThumbnailProvider`](https://developer.apple.com/documentation/quicklook/qlthumbnailprovider)
* [`QLThumbnailReply`](https://developer.apple.com/documentation/quicklook/qlthumbnailreply)
