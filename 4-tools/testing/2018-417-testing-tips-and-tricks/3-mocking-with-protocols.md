3-mocking-with-protocols.md



## [Mocking with protocols](3-mocking-with-protocols.md) | | p105




- Classes often interact with other classes in app or SDK
- Many SDK classes cannot be created directly
- Delegate protocols make testing more challenging
- Solution: Mock interface of external class using protocol

```swift
class CurrentLocationProvider: NSObject {
    var currentLocationCheckCallback: ((CLLocation) -> Void)?
    func checkCurrentLocation(completion: @escaping (Bool) -> Void) {
        self.currentLocationCheckCallback = { [unowned self] location in
            completion(self.isPointOfInterest(location))
}
        locationManager.requestLocation()
    }
    func isPointOfInterest(_ location: CLLocation) -> Bool {
        // Perform check...
} 
}
```


### Mocking Using a Subclass

- Subclassing the external class in tests and overriding methods
- Can work, but risky
- Some SDK classes cannot be subclassed
- Easy to forget to override methods


### Mocking with Protocols
Recap

- Define a protocol representing the external interface
- Define extension on the external class conforming to the protocol
- Replace all usage of external class with the protocol
- Set the external reference via initializer or a property, using the protocol type

### Mocking Delegates with Protocols
Recap

- Define delegate protocol with interfaces your code implements
- Replace subject type with mock protocol defined earlier
- In mock protocol, rename delegate property
- In extension on original type, implement mock delegate property and convert

