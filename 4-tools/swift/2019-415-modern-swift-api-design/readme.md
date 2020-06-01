



## [2019 415 Modern Swift API Design](https://developer.apple.com//videos/play/wwdc2019/415/)



- Ben Cohen, Swift Team 
- Doug Gregor, Swift Team


Topic|Speaker|Time|Page
--|--|--|--
Values and references|Ben Cohen||p
Protocols and generics|Ben Cohen|12:20|p
Key path member lookup: SE-0252|Ben Cohen|20:00-|p80
Property wrappers: SE-0258|Doug Gregor|23:30-|p97


## Values and references

type vs semantics

x

## Protocols and generics [12:20]




### Key Path Member Lookup

• Swift Evolution: [SE-0252](https://github.com/apple/swift-evolution/blob/master/proposals/0252-keypath-dynamic-member-lookup.md)


forward-on properties

```swift
@dynamicMemberLookup
struct GeometricVector<Storage: SIMD> where Storage.Scalar:     FloatingPoint {
    var value: Storage
    init(_ value: Value) { self.value = value }
    }
    subscript(dynamicMember keyPath: KeyPath<Storage, Scalar>) -> Scalar {
        value[keyPath: keyPath]
    }
}
```

properties with logic

```swift
@dynamicMemberLookup
struct Material {
    public var roughness: Float
    public var color: Color
    private var _texture: Texture
    public subscript<T>(dynamicMember keyPath: ReferenceWritableKeyPath<Texture, T>) -> T {
        get { _texture[keyPath: keyPath] }
        set {
            if !isKnownUniquelyReferenced(&_texture) { 
                _texture = Texture(copying: _texture) 
            }
            _texture[keyPath: keyPath] = newValue
        }
    } 
}
```



