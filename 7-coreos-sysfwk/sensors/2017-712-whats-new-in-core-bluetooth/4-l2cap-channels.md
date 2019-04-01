
## [L2CAP Channels](4-l2cap-channels.md) | | p57


### L2CAP Connection Oriented Channels

- Bluetooth SIG Protocol underlying all communication
- Logical Link Control and Adaptation Protocol
- Stream between two devices
- Introduced for LE in Bluetooth Core Spec 4.1


### Central Side L2CAP
Open an L2CAP Channel on an existing CBPeripheral connection

```swift
open class CBPeripheral: CBPeer {
    open func openL2CAPChannel(_ PSM: CBL2CAPPSM)
}

public protocol CBPeripheralDelegate: NSObjectProtocol { 
    optional public func peripheral(_ peripheral: CBPeripheral, 
        didOpen channel: CBL2CAPChannel?, error: Error?)
}
```



### PSM

- SIG Specified PSM for standardized profiles
- Locally assigned PSM for dynamic services

```swift
/*!
 * @const CBUUIDL2CAppSMCharacteristicString
 * @discussion The PSM (a little endian uint16_t) of an L2CAP Channel associated with the GATT service
 * containing this characteristic. Servers can publish this characteristic with the UUID
 * ABDD3056-28FA-441D-A470-55A75A52553A */
public let CBUUIDL2CAppSMCharacteristicString: String
```



### Peripheral Side L2CAP

Listen for incoming L2CAP Channels

```swift
open class CBPeripheralManager : CBManager {
    open func publishL2CAPChannel(
        withEncryption encryptionRequired: Bool) 
    open func unpublishL2CAPChannel(_ PSM: CBL2CAPPSM)
}
public protocol CBPeripheralManagerDelegate : NSObjectProtocol {
    optional public func peripheralManager(
        _ peripheral: CBPeripheralManager, 
        idPublishL2CAPChannel PSM: CBL2CAPPSM, 
        error: Error?)
}
```


### Opening an L2CAP Channel

optional public func peripheralManager(_ peripheral: CBPeripheralManager, didPublishL2CAPChannel PSM: CBL2CAPPSM, error: Error?)

optional public func peripheralManager(_ peripheral: CBPeripheralManager, didOpen channel: CBL2CAPChannel?, error: Error?)


```swift
@available(macOS 10.13, iOS 11.0, *) 
open class CBL2CAPChannel: NSObject {
    open var peer: CBPeer! { get }
    open var inputStream: InputStream! { get } 
    open var outputStream: OutputStream! { get } 
    open var psm: CBL2CAPPSM { get }
}
```


### Stream Events

Stream events are delivered through NSStream

```swift
public protocol StreamDelegate: NSObjectProtocol {
    optional public func stream(_ aStream: Stream, handle eventCode: Stream.Event)
}
public struct Stream.Event: OptionSet {
    public static var openCompleted: Stream.Event { get } 
    public static var hasBytesAvailable: Stream.Event { get } 
    public static var hasSpaceAvailable: Stream.Event { get } 
    public static var errorOccurred: Stream.Event { get } 
    public static var endEncountered: Stream.Event { get }
}
```

### Closing Channels

Channels may be closed due to

- Link loss
- Central close
- Peripheral unpublished
- Peripheral object is released



### When Should L2CAP Be Used?

- Use GATT where it makes sense
- Lowest overhead
- Best performance
- Best for large data transfers
- Great for stream protocols

