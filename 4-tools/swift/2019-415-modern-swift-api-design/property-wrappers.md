
•Property Wrappers
• Swift Evolution: [SE-0258](https://github.com/apple/swift-evolution/blob/master/proposals/0258-property-wrappers.md)


lazy var - is one instance of general pattern


Property Wrappers

```swift
public struct MyType {
    @LateInitialized public var text: String
}
```

- Capture backing storage property and access policy for re-use
- Provides similar benefits to the built-in lazy
  - Eliminates boilerplate
  - Documents semantics at the point of definition


```swift
// Implementing a Property Wrapper
@propertyWrapper
public struct LateInitialized<Value> {
    private var storage: Value?


    public init() { storage = nil }
    public var value: Value {
        get {
            guard let value = storage else {
                fatalError("value has not yet been set!")
            }
            return value
        }
        set { storage = newValue }
    }
}
```



Using Property Wrappers
Uses of property wrappers expand into a stored property and a computed property
```swift
public struct MyType {
    @LateInitialized public var text: String
}
```


```swift
// Defensive Copying
@propertyWrapper
public struct DefensiveCopying<Value: NSCopying> {
    private var storage: Value
    public init(initialValue value: Value) {
        storage = value.copy() as! Value

    }
    
    public var value: Value {
        get { storage }
        set {
            storage = newValue.copy() as! Value
        }
    } 
}

```swift




Using the DefensiveCopying Property Wrapper @DefensiveCopying variables can be initialized in their declaration:

```swift
public struct MyType {
@DefensiveCopying public var path: UIBezierPath = UIBezierPath()
}
```


#### Using the DefensiveCopying Property Wrapper

```swift
extension DefensiveCopying {
    public init(withoutCopying value: Value) {
        storage = value
    }
}
```

Initializing the backing storage property:
```swift
public struct MyType {
    @DefensiveCopying(withoutCopying: UIBezierPath())
    public var path: UIBezierPath
}
```



API Design with Property Wrappers
Property wrappers describe the policy behind your data access Lots of API revolves around data access

```swift
@UserDefault(key: "BOOSTER_IGNITED", defaultValue: false) static var isBoosterIgnited: Bool

@ThreadSpecific var localPool: MemoryPool

@Option(shorthand: "m", documentation: "Minimum value", defaultValue: 0)  var minimum: Int
```




Property Wrappers in SwiftUI
View data dependencies are expressed using property wrappers


```swift
struct SlideViewer: View {
    @State private var isEditing = false
    @Binding var slide: Slide
    var body: some View { 
        VStack {
            Text("Slide #\(slide.number)")
            if isEditing {
                TextField($slide.title) 
            }
// ...  
        }
    } 
}
```