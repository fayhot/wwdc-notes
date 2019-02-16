## [5. Classes and generics](classes-and-generics.md)| Doug | 4825 | p137

classes-and-generics.md



### Liskov Substitution Principle


If S is a subtype of T, any instance of type T can be replaced by an instance of S

```swift
class Vehicle { ... }
class Taxi: Vehicle { ... } 
class PoliceCar: Vehicle { ... } 
extension Vehicle {
    func drive() { ... } 
}
taxi.drive()
```


https://en.wikipedia.org/wiki/Barbara_Liskov


### Protocol Conformances and Classes

- Protocol conformances are inherited by subclasses
- A single conformance must work for all subclasses

```swift
// Initializer Requirements 

protocol Decodable {
    init(from decoder: Decoder) throws 
}


extension Decodable {
    static func decode(from decoder: Decoder) throws -> Self {
        return try self.init(from: decoder)
    }
}


class Vehicle : Decodable {
    init(from decoder : Decoder) throws { }
}

Taxi.decode(from: decoder) // produces a Taxi
```

### Which Initializer Gets Called?.

Final Classes Have No Subclasses
final classes are exempt from these rules
Use final when your class is not customizable through inheritance