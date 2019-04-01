
## [Enhanced Reliability](2-enhanced-reliability.md) | p20

### Backgrounded Apps

iOS Apps can continue using Core Bluetooth in the background


### CBCentralManager restoration

Central operations can continue when your app is not running

- Scan for new devices with services
- Connect to an already known device



### CBPeripheralManager Restoration
Peripheral operations can continue when your app is not running

- Publish local services
- Advertise service UUID


### State Preservation and Restoration (NEW)

Works across device reboot or Bluetooth system events

- Try to ask for as few system resources as possible 
- Background activities will be stopped if
  - User force quits the app
  - User disables Bluetooth



### Write Without Response (NEW)

Write Without Response would be dropped due to memory pressure

New property will tell your app if more data can be sent


```swift
open class CBPeripheral: CBPeer {
    open var canSendWriteWithoutResponse: Bool { get }
}
public protocol CBPeripheralDelegate: NSObjectProtocol {
    optional public func peripheralIsReady(toSendWriteWithoutResponse peripheral: CBPeripheral) 
}

```
