# [2019 231 Integrating SwiftUI](https://developer.apple.com//videos/play/wwdc2019/231/)


- Tanu Singhal, UIKit 
- Raleigh Ledet, AppKit



Topic|Speaker|Time
--|--|--
Hosting SwiftUI views in your app|Tanu Singhal
Embedding existing views in SwiftUI|Tanu Singhal
Integrating your data model | Raleigh Ledet
Integrating with the system | Raleigh Ledet





## Hosting SwiftUI views in your app


## Embedding existing views in SwiftUI


[`UIViewControllerRepresentable`](https://developer.apple.com/documentation/swiftui/uiviewcontrollerrepresentable)

[`UIViewRepresentable`](https://developer.apple.com/documentation/swiftui/uiviewrepresentable)

### Advanced

- 


[`UIViewControllerRepresentableContext`](https://developer.apple.com/documentation/swiftui/uiviewcontrollerrepresentablecontext)

### Demo - Ratings


## Integrating your data model

data type|DataModel|SwiftUI
--|--|--
Static Data - one shot|
Dynamic Data|DataModel : BindableObject; var didChange: PublisherType|@ObjectBinding var data : DataModel
SwiftUI write back to data||$data

[ObservableObject](https://developer.apple.com/documentation/combine/observableobject)

### Demo: PlantsDataModel


[NotificationCenter.Publisher](https://developer.apple.com/documentation/foundation/notificationcenter/publisher)


[`NSObject.KeyValueObservingPublisher`](https://developer.apple.com/documentation/objectivec/nsobject/keyvalueobservingpublisher)

## Integrating with the system


---


[Framework Integration](https://developer.apple.com/documentation/swiftui/framework_integration) 28:25


[`NSItemProvider`](https://developer.apple.com/documentation/foundation/nsitemprovider)

Drag and Drop

Paste

Focus

Undo and Redo


Objective-C Integration


