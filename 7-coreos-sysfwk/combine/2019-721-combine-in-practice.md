[2019 721 Combine in Practice](https://developer.apple.com//videos/play/wwdc2019/721/)

```swift
protocol Publisher { 
    associatedtype Output 
    associatedtype Failure: Error
 
    func subscribe<S: Subscriber>(_ subscriber: S) 
    where S.Input == Output, S.Failure == Failure
}
```

Publisher|Output|Failure
--|--|--
publisher(for: .newTrickDownloaded)|Notification|Never
.map {$0 .userInfo?["data"] as! Data }|Data|Never
.tryMap |MagicTrick|Error
.decode|MagicTrick|Error
.assertNoFailure()|



## Failure Handling Operators

- assertNoFailure
- retry
- catch
- mapError
- setFailureType




## Flat Map


```swift
.flatMap { data in
    return Just(data)
        .decode(MagicTrick.self, JSONDecoder())
        .catch {
            return Just(MagicTrick.placeholder)
        } 
}
```

Publisher|Output|Failure
--|--|--
above|MagicTrick|Never
.publisher(for: \.name)|String|Never



## Scheduled Operators

- Scheduler describes
  - When / Where
- Supported by RunLoop and DispatchQueue


Scheduled Operators

- delay
- debounce
- throttle
- receive(on:)
- subscribe(on:)



Publishers
```
Recipe for an event stream
Operators describe new publishers from existing Strongly typed values/errors over time
Can be synchronous or asynchronous
Can attach compatible Subscribers
```


```swift
protocol Subscriber {
     
    associatedtype Input 
    associatedtype Failure: Error

    func receive(subscription: Subscription)
    func receive(_ value: Subscribers.Demand)
    func receive(completion: Subscribers.Completion<Failure>)
}
```



Kinds of Subscribers

```
Key Path Assignment
Sinks
Subjects
SwiftUI
```

Cancellation

- Built into Combine
- Terminate subscriptions early
 
```swift
protocol Cancellable { func cancel()
}
final class AnyCancellable: Cancellable {} // Calls `cancel` on deinit
```



Subjects

- Behave like both Publisher and Subscriber
- Broadcast values to multiple subscribers

```swift
protocol Subject: Publisher, AnyObject {
    func send(_ value: Output)
    func send(completion: Subscribers.Completion<Failure>)
}
```

```swift
// Combine with SwiftUI
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


Combine
Many built in
Publishers Subscribers Subjects
Common functionality in over 90 operators




•Integrating Combine

Ben D. Jones, Foundation




