
# [2017 712 What's New in Core Bluetooth](https://developer.apple.com/videos/play/wwdc2017/712)

Since iOS 5 / Year 2011

Support tvOS and WatchOS in 2017


2017-712-whats-new-in-core-bluetooth/readme.md

- Craig Dooley, Bluetooth Engineer
- Duy Phan, Bluetooth Engineer

Topic|X
---|---
• Introduction
• Enhanced reliability
• Platform support
• L2CAP channels
• Best practices
• Getting the most out of Core Bluetooth


## Built-in Profiles

- Apple Notification Center Service
- Apple Media Service
- MIDI over Bluetooth Low Energy
- iBeacon
- Current Time Service
- HID Over GATT



### Reading Characteristics as a Central

- Services can be read from a connected Central
- Retrieve by identifier Retrieve connected devices

```swift
open class CBCentralManager : CBManager {
    open func retrievePeripherals(withIdentifiers identifiers: [UUID]) -> [CBPeripheral]
    open func retrieveConnectedPeripherals(withServices serviceUUIDs: [CBUUID]) -> [CBPeripheral] 
}
```
