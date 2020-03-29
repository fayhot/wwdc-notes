2019-723-advance-in-foundation.md


[2019 723 Advances in Foundation](https://developer.apple.com/videos/play/wwdc2019/723/)



- Ordered Collection Diffing
- Data
- Units and Formatters
- OperationQueue
- USB and SMB on iOS
- Swift Update




## Ordered Collection Diffing

[`CollectionDifference`](https://developer.apple.com/documentation/swift/collectiondifference)


[`String`](https://developer.apple.com/documentation/swift/string)

```swift
func applying(_ difference: CollectionDifference<Character>) -> String?


unc difference<C>(from other: C) -> CollectionDifference<Character> where C : BidirectionalCollection, Self.Element == C.Element

func difference<C>(from other: C, by areEquivalent: (C.Element, Character) -> Bool) -> CollectionDifference<Character> where C : BidirectionalCollection, Self.Element == C.Element
```

[`Array`](https://developer.apple.com/documentation/swift/array)

```swift
func applying(_ difference: CollectionDifference<Element>) -> Array<Element>?


func difference<C>(from other: C) -> CollectionDifference<Element> 
where C : BidirectionalCollection, Self.Element == C.Element


func difference<C>(from other: C, by areEquivalent: (C.Element, Element) -> Bool) -> CollectionDifference<Element> 
where C : BidirectionalCollection, Self.Element == C.Element

```

## Data

### Compressions

## Units and Formatters


## OperationQueue

## USB and SMB on iOS


[2019 719 What’s New in File Management and Quick Look](https://developer.apple.com/videos/play/wwdc2019/719)


## Swift Update