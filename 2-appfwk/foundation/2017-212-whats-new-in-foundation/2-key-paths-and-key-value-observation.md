
## [Key Paths and Key Value Observation - Michael LeHew, Foundation](212-2-key-paths-and-key-value-observation.md) (5~23.5)


### Swift 3 - Intro

### Key Paths

* Property traversal
*  Statically type-safe
* Fast
* Applicable to all values
* Works on all platforms
* [SE-0161 Smart KeyPaths: Better Key-Value Coding for Swift](https://github.com/apple/swift-evolution/blob/master/proposals/0161-key-paths.md)


#### Creating Key Paths

`\Kid.nickname`

Backslash , Dot, Base Type, PropertyName

`\Data.[.startIndex] \.[.startIndex]`


### Uniform Syntax

Types | Properties/Subscripts
--|--
struct | let/var
class | get/set
`@objc class` | stored and computed

### Using Key Paths

`let age = ben[keyPath: \Kid.age]`

#### Birthday Party


#### Appending Key Paths

`\BirthdayParty.celebrant.appending(\Kid.age)`


#### Type Eresed Key paths

`let partyPaths = [\BirthdayParty.theme, BirthdayParty.attending, \BirthdayParty.celebrant]`



### API

* [`AnyKeyPath`](https://developer.apple.com/documentation/swift/anykeypath)
* [`PartialKeyPath<Root>`](https://developer.apple.com/documentation/swift/partialkeypath)
* [`KeyPath<Root, Value>`](https://developer.apple.com/documentation/swift/keypath)
* [`WritableKeyPath<Root, Value>`](https://developer.apple.com/documentation/swift/writablekeypath)
* [`ReferenceWritableKeyPath<Root, Value>`](https://developer.apple.com/documentation/swift/referencewritablekeypath)


WritableKeyPath - Write directly into value-type base (inout/mutating)

ReferenceWritableKeyPath - Write into a reference-type base


### Key Value Observing


`let observation = mia.observe(\.age) { ... }`

observation - 2 functions. avoid void* context ; manage life cycle.


```swift
let observation = mia.observe(\.age) {
  observed : Kid, change : NSKeyValueObservedChange<Double> in


}
```
