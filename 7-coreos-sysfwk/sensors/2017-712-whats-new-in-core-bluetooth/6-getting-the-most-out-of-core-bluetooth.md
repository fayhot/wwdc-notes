

## [Getting the Most out of Core Bluetooth](6-getting-the-most-out-of-core-bluetooth.md) | Duy Phan |  | p91


1MB = 3,240 seconds 2.5 kbps

### Protocol Overhead

L2CAP (4 Bytes) + ATT (3 Bytes) + Attribute Data (20 Bytes)

### Write With Response


### Write Without Response

- Reliable with Core Bluetooth flow control
- Use all available connection events to transmit
- Takes advantage of larger Connection Event Length

Default MTU

37 kbps

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

### L2CAP Connection Oriented Channels

197 kbps

L2CAP (4 Bytes) + Attribute Data (147 Bytes)

### Faster Connection Interval

L2CAP + EDL

394 kbps



### Throughput (kbps)

X|Y
---|---
Write With Response|2.5
Write Without Response|5.2
Packed CE Length, Default MTU|37
Larger MTU|48
EDL|135
L2CAP + EDL|197 
L2CAP + EDL + 15ms Int|394


### Summary

- Request a shorter Connection Interval
- Take advantage of GATT optimizations
- Use L2CAP Channel for large transfers and stream protocols
- Update your hardware (4.2 EDL, 5.0) for best performance and battery life