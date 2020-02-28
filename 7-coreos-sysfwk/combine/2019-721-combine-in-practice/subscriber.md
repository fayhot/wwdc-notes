
## [Subscriber](subscriber.md)

```swift
protocol Subscriber {
     
    associatedtype Input 
    associatedtype Failure: Error

    func receive(subscription: Subscription)
    func receive(_ value: Subscribers.Demand)
    func receive(completion: Subscribers.Completion<Failure>)
}
```


### Kinds of Subscribers

```
Key Path Assignment
Sinks
Subjects
SwiftUI
```


### Cancellation

- Built into Combine
- Terminate subscriptions early
 
```swift
protocol Cancellable { 
    func cancel()
}
final class AnyCancellable: Cancellable {} // Calls `cancel` on deinit
```



### 3. Subjects

- Behave like both Publisher and Subscriber
- Broadcast values to multiple subscribers

```swift
protocol Subject: Publisher, AnyObject {
    func send(_ value: Output)
    func send(completion: Subscribers.Completion<Failure>)
}
```

### 4. Combine with SwiftUI

```swift

class WizardModel : BindableObject {
    var trick: WizardTrick { didSet { didChange.send() }
    var wand: Wand? { didSet { didChange.send() }
    let didChange = PassthroughSubject<Void, Never>() 
}


struct TrickView: View {
    @ObjectBinding var model: WizardModel

    var body: some View {
        Text(model.trick.name)
    }
}
```


----


Refs

