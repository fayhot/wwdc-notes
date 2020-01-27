operator.md


## [Operators](operator.md)

## Failure Handling Operators

operator|publisher
--|--
assertNoFailure|[Publishers.AssertNoFailure](https://developer.apple.com/documentation/combine/publishers/assertnofailure)
retry|[Publishers.Retry](https://developer.apple.com/documentation/combine/publishers/retry)
catch|[Publishers.Catch](https://developer.apple.com/documentation/combine/publishers/catch)
mapError|[Publishers.MapError](https://developer.apple.com/documentation/combine/publishers/maperror)
setFailureType|[Publishers.SetFailureType](https://developer.apple.com/documentation/combine/publishers/setfailuretype)
x|[Publishers.TryCatch](https://developer.apple.com/documentation/combine/publishers/trycatch)



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
.flatMap|MagicTrick|Never
.publisher(for: \.name)|String|Never



## Scheduled Operators

- Scheduler describes
  - When / Where
- Supported by RunLoop and DispatchQueue


Scheduled Operators

operator|struct|description
--|--|--
delay|[Publishers.Delay](https://developer.apple.com/documentation/combine/publishers/delay)|delays delivery of elements and completion to the downstream receiver.
debounce|[`Publishers.Debounce`](https://developer.apple.com/documentation/combine/publishers/debounce)|publishes elements only after a specified time interval elapses between events.
throttle|[Publishers.Throttle](https://developer.apple.com/documentation/combine/publishers/throttle)|publishes either the most-recent or first element published by the upstream publisher in a specified time interval.
receive(on:)|
subscribe(on:)|
x|[Publishers.MeasureInterval](https://developer.apple.com/documentation/combine/publishers/measureinterval)|measures and emits the time interval between events received from an upstream publisher.
x|[Publishers.Timeout](https://developer.apple.com/documentation/combine/publishers/timeout)


