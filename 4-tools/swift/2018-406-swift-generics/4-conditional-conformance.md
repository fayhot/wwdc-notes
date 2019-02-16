

## [4. Conditional conformance ](4-conditional-conformance.md)| Doug | 2700 | p83


### Conditional Conformance to BidirectionalCollection

Conformance depends on additional requirements

```swift
extension Slice: BidirectionalCollection where Base: BidirectionalCollection {  
    func index(before idx: Index) -> Index { return base.index(before: idx) } 
}

extension Slice: RandomAccessCollection where Base: RandomAccessCollection {
    func index(_ idx: Index, offsetBy n: Int) -> Index { return base.index(idx, offsetBy: n) }
    func distance(from s: Index, to e: Index) -> Int { return base.distance(from: s, to: e) }
}

```

### Range as a Collection

Range conditionally conforms to RandomAccessCollection

```swift
Range conditionally conforms to RandomAccessCollection
extension Range: Collection, BidirectionalCollection, RandomAccessCollection        where Bound: Strideable, Bound.Stride: SignedInteger {

    // ...
} 
```

CountableRange is a convenient alias for Ranges that are Collections

```swift
typealias CountableRange<Bound: Strideable> = Range<Bound>
    where Bound.Stride: SignedInteger
```

