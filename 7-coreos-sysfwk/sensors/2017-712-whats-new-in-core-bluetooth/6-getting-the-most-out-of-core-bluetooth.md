

## [Getting the Most out of Core Bluetooth](6-getting-the-most-out-of-core-bluetooth.md) | Duy Phan, Bluetooth Engineer | p91




1MB = 3,240 seconds 2.5 kbps

Protocol Overhead

Write With Response


### Write Without Response

- Reliable with Core Bluetooth flow control
- Use all available connection events to transmit
- Takes advantage of larger Connection Event Length



### Fitting your data

- Apple devices determine the optimal MTU
- Accessories should support a large MTU
- Use large attributes aligned to MTU

```swift
open class CBPeripheral: CBPeer {
open func maximumWriteValueLength(for type: CBCharacteristicWriteType) -> Int
}
open class CBCentral: CBPeer {
open var maximumUpdateValueLength: Int { get }
}
```



### Extended Data Length


- New Feature in Bluetooth 4.2
- Much larger packets (251 vs 27 bytes)
- Transparent to the application
- 4x throughput with the same radio time
- Available on iPhone 7 and Apple Watch Series 2


### Faster Connection Interval

L2CAP + EDL

394 kbps


Throughput (kbps)

### Summary

- Request a shorter Connection Interval
- Take advantage of GATT optimizations
- Use L2CAP Channel for large transfers and stream protocols
- Update your hardware (4.2 EDL, 5.0) for best performance and battery life