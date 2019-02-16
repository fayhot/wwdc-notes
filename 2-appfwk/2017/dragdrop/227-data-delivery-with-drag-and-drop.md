# [2017 227 Data Delivery with Drag and Drop](https://developer.apple.com/videos/play/wwdc2017/227/)

* Dave Rahardja, UIKit
* Tanu Singhal, UIKit

TOC

* NSItemProvider Basics
* Uniform Type Identifiers
* Model Classes
* Advanced Topics

## NSItemProvider Basics

[`NSItemProvider`](https://developer.apple.com/documentation/foundation/nsitemprovider) since iOS 8

### NSItemProvider

Data promises
Asynchronous Progress, cancellable
Supported
Drag and Drop
UIPasteConfiguration UIPasteboard


### Demo


### Progress and Cancellation

Maximize Compatibility


## Uniform Type Identifiers


### Multiple Representations

One NSItemProvider = one “thing” being dragged
Multiple representations
Vector drawing

Native file format — com.yourcompany.vector-drawing PDF — kUTTypePDF
PNG — kUTTypePNG
JPG — kUTTypeJPEG


### Fidelity Order
Highest fidelity first
Internal type
Highest fidelity common type Next highest fidelity common type ...


### Use Concrete Uniform Type Identifiers
Abstract item
public.data public.plain-text public.image
Concrete data
public.utf8-plain-text public.png
Private type identifier
com.yourcompany.vector-drawing




## Model Classes

### NSItemProviderReading, -Writing Protocols

* NSItemProviderWriting — exports data from model object
* NSItemProviderReading — creates model object from data
* Maintained with model classes, not UI code


### [`NSItemProviderWriting`](https://developer.apple.com/documentation/foundation/nsitemproviderwriting) Protocol (New in iOS 11)

5 = 3 (methods/properties) + 2 (static methods/properties)

### [`NSItemProviderReading`](https://developer.apple.com/documentation/foundation/nsitemproviderreading) Protocol (New in iOS 11)

`static func object(withItemProviderData data: Data,
    typeIdentifier: String) throws -> Self`

x

`static var readableTypeIdentifiersForItemProvider: [String] { get }`

### Model Classes

Conform to NSItemProviderReading, Writing
NSObject
Drag and Drop, UIPasteConfiguration, UIPasteboard

### Demo 2


## Advanced Topics

### Data Marshaling


### Progress and Cancellation

### Per-Representation Visibility

### Team Data


teamData property
Up to 8 KB of metadata Visible to same Team Improve UI during drag


Suggested Name
suggestedName property Used as file name
Use when providing NSData

Preferred Presentation Size
preferredPresentationSize property Use to target drop animation


### File Provider

* App extension
* Allows app to be terminated
* URL to file in File Provider container
* Open in Place

* Building Great Document-based Apps in iOS 11
* File Provider Enhancements


### Demo 3


## Summary

* NSItemProvider
* Multiple representations Asynchronous Progress, cancellable
* NSItemProviderReading and Writing Visibility and Team Data
* File Provider, Open in Place
