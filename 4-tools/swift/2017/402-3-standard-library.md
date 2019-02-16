



## Swift Strings

• Faster, easier character processing

Ben Cohen, Swift Standard Library Team

e ́

* 0xE9
* 0x65 0x301


### Unicode Correctness by Default

In Swift, a Character is a grapheme

### Faster Character Processing

Benchmark for Latin-derived characters, Han ideographs, and Kana


#### // SE-0172: Simpler One-Sided Slicing Syntax

values[i...]

### Swift Strings Have Three Properties

### Owner Reference Count Drops to Zero
Owner is freed, frees the string buffer

#### Creating a Substring


[StringProtocol](https://developer.apple.com/documentation/swift/stringprotocol)

#### // SE-0168: Multi-line String Literals

### New Generics Features



#### // Extending Sequence // SE-0142: Swift 4 Sequence

```swift
protocol Sequence {
associatedtype Element
associatedtype Iterator: IteratorProtocol where Iterator.Element == Element
 func makeIterator() -> Iterator
 }
```

// Redundant constraints

#### // SE-0148: Generic Subscripts // Use case: partial ranges


#####

struct PartialRangeFrom<Bound: Comparable> {
 let lowerBound: Bound
}


[RangeExpression](https://developer.apple.com/documentation/swift/rangeexpression)

### More Standard Library Features

```

SE-0104 Protocol-oriented integers
SE-0153 Dictionary & Set enhancements
SE-0163 Improved String C Interop and Transcoding
SE-0170 NSNumber bridging and Numeric types
SE-0173 Add MutableCollection.swapAt(\_:\_:)
SE-0174 Change filter to return Self for RangeReplaceableCollection
```
