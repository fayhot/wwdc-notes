

# [2018 406 Swift Generics](https://developer.apple.com/videos/play/wwdc2018/406/)

2018-406-swift-generics/readme.md


- Ben Cohen, Swift Standard Library
- Doug Gregor, Swift Compiler


https://docs.swift.org/swift-book/LanguageGuide/Generics.html


Swift|Generic features
---|---
4.1|Conditional conformance<br/>Recursive constraints
4.0|Associated type where clauses<br/> Generic subscripts
3.1|Nested generic types<br/> Concrete type constraints
3.0|Protocol operators<br/> Generic typealiases
2.0|Protocol extensions<br/> Default implementations
1.0|Generic types<br/> Generic functions



Topic|Speaker|Time|Page
---|---|---|--
What are generics?
Protocol design
Protocol inheritance
Conditional conformance | | 2700
Recursive Constraints (Extended)|
Classes and generics| Doug | 4825 | p137
Summary||4030




## 2. Designing a Protocol | Ben | | p27



```swift
// Different Kinds of Collections

struct Buffer<Element> {
    let count : Int 

    subscript(at: Int) -> Element
}
```






```swift
// Constraining Index
protocol Collection {

    associatedtype Element
    associatedtype Index
}

```

### Customization Points

// Slow Count

// Speedy Count


// Using Count in a Generic Context


protocol Collection {
    var count : Index { get }
}

// default implemention of `var count` may be not opmotized for specific type.


## [3. Protocol inheritance](3-protocol-inheritance.md) | Doug | 2045 | p59


## [4. Conditional conformance ](4-conditional-conformance.md)| Doug | 2700 | p83


## [Recursive Constraints](recursive-constraints.md) | ? | 3330 | p96

## [5. Classes and generics](classes-and-generics.md)| Doug | 4825 | p137




## Summary

- Swift’s generics provide code reuse while maintaining static type information
- Let the push-pull between generic algorithms and conforming types guide design
  - Protocol inheritance captures specialized capabilities of some conforming types 
  - Conditional conformance provides composition for those capabilities
- Apply the Liskov Substitution Principle when working with classes

