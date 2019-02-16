
## [Mocking with protocols](3-mocking-with-protocols.md) | Stuart | 1950 | p105


- Classes often interact with other classes in app or SDK
- Many SDK classes cannot be created directly
- Delegate protocols make testing more challenging
- Solution: Mock interface of external class using protocol



### Mocking Using a Subclass

- Subclassing the external class in tests and overriding methods
- Can work, but risky
- Some SDK classes cannot be subclassed
- Easy to forget to override methods


```swift
class CurrentLocationProvider: NSObject {
    var locationFetcher: LocationFetcher
    init(locationFetcher: LocationFetcher = CLLocationManager()) {
        self.locationFetcher = locationFetcher
        super.init()
        self.locationFetcher.desiredAccuracy = kCLLocationAccuracyHundredMeters
        self.locationFetcher.delegate = self
    } 
}

protocol LocationFetcher {
    var delegate: CLLocationManagerDelegate? { get set }
    var desiredAccuracy: CLLocationAccuracy { get set }
    func requestLocation()
}
extension CLLocationManager: LocationFetcher {}

```


---


```swift

protocol LocationFetcher {
    var locationFetcherDelegate: LocationFetcherDelegate? { get set }
    // ...
}
protocol LocationFetcherDelegate: class {
    func locationFetcher(_ fetcher: LocationFetcher, didUpdateLocations locs: [CLLocation])
}
class CurrentLocationProvider: NSObject {
    var locationFetcher: LocationFetcher
    init(locationFetcher: LocationFetcher = CLLocationManager()) {
// ...
        self.locationFetcher.delegate = self
    }
}

```



### Mocking with Protocols - Recap

- Define a protocol representing the external interface
- Define extension on the external class conforming to the protocol
- Replace all usage of external class with the protocol
- Set the external reference via initializer or a property, using the protocol type


### Mocking Delegates with Protocols - Recap

- Define delegate protocol with interfaces your code implements
- Replace subject type with mock protocol defined earlier
- In mock protocol, rename delegate property
- In extension on original type, implement mock delegate property and convert

