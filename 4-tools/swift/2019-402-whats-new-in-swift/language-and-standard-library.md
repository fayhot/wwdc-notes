
## Language and Standard Library - Anna Zaks, Swift Team


https://apple.github.io/swift-evolution/


### Implicit return from single expressions | [SE-0255](https://github.com/apple/swift-evolution/blob/master/proposals/0255-omit-return.md)

```swift
struct Rectangle {
    var width = 0.0, height = 0.0
    var area: Double { width * height }
}
```

### [SE-0242](https://github.com/apple/swift-evolution/blob/master/proposals/0242-default-values-memberwise.md)  Synthesized default values for the memberwise initializer
// Proposal and implementation by an open source contributor Alejandro Alonso
// Swift Evolution:

```swift
struct Dog {
    var name = "Generic dog name"
    var age = 0
}

```

### SIMD — A Better API for Vector Programming
Swift Evolution: SE-0229





### [SE-0228](https://github.com/apple/swift-evolution/blob/master/proposals/0228-fix-expressiblebystringinterpolation.md) : New Design for String Interpolation
Up to 1.7x faster than Swift 4.2’s design Extend String with new interpolation behaviors
Support in your own types by conforming to [`ExpressibleByStringInterpolation`](https://developer.apple.com/documentation/swift/expressiblebystringinterpolation) protocol





### [SE-0244](https://github.com/apple/swift-evolution/blob/master/proposals/0244-opaque-result-types.md): Opaque Result Types


Use when API returns the same type but is leaking implementation details
Requires new Swift runtime support
Available on macOS Catalina, iOS 13, tvOS 13, watchOS 6 and later
Guard uses with availability checking when deploying to earlier OS releases


### Property Wrapper Types | SE-0258

Reuse code for property access patterns
Lazily initialized values Thread-local storage
Copy on write objects
Data dependencies in SwiftUI User defaults




Wrapper types define custom access patterns
Property can adopt by adding an attribute to its declaration



Swift DSL is waiting for your feedback!


https://forums.swift.org/c/evolution