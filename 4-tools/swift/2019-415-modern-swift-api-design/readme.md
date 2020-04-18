2019-415-modern-swift-api-design/readme.md

2019-415-modern-swift-api-design/readme.md


## [2019 415 Modern Swift API Design](https://developer.apple.com//videos/play/wwdc2019/415/)



- Ben Cohen, Swift Team 
- Doug Gregor, Swift Team


Topic|Speaker|Time|Page
--|--|--|--
Values and references|Ben Cohen||p
Protocols and generics|Ben Cohen|12:20|p
Key path member lookup: SE-0252|Ben Cohen||p80
Property wrappers: SE-0258|Doug Gregor|23:30-|p97


## Values and references

type vs semantics

x

## Protocols and generics [12:20]




Key Path Member Lookup

• Swift Evolution: SE-0252





```swift
@dynamicMemberLookup
struct Material {
    public var roughness: Float
    public var color: Color
    private var _texture: Texture
    public subscript<T>(dynamicMember keyPath: ReferenceWritableKeyPath<Texture, T>) -> T {
        get { _texture[keyPath: keyPath] }
        set {
            if !isKnownUniquelyReferenced(&_texture) { _texture = Texture(copying: _texture) }
            _texture[keyPath: keyPath] = newValue
        }
    } 
}
```



