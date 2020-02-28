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


## See [Operators](operator.md)

---



Publishers
```
Recipe for an event stream
Operators describe new publishers from existing Strongly typed values/errors over time
Can be synchronous or asynchronous
Can attach compatible Subscribers
```

## See [Subscriber](subscriber.md)



Combine

- Many built in
- Publishers Subscribers Subjects
- Common functionality in over 90 operators



## [Integrating Combine](integrating.md) 22:50