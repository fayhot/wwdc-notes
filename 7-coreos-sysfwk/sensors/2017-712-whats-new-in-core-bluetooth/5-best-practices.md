

## [Best Practices](5-best-practices.md)  | p76

### Follow the Bluetooth Accessory  Design Guidelines for Apple Products


### Use Existing Profiles and Services


### Why does it take so long to connect?


### Time to Discover




### Connection Speed

- Use the shortest advertising interval possible
- Optimize for when users are trying to use your accessory
- See the Bluetooth Accessory Design Guidelines for power-efficient advertising intervals


### Reconnecting devices
No need to scan for a peripheral for reconnect Retrieve the peripheral and directly connect

```swift
let identifier = UUID()
let peripherals = central.retrievePeripherals(withIdentifiers: [ identifier ]) 
central.connect(peripherals[0])
```


### Service Discovery Speed

- Use as few services/characteristics as possible Group services by UUID size
- Support GATT Caching
- Use “Service Changed”


### New Accessory Recommendations

- Use the newest chipset / Bluetooth standard available 4.2 and 5.0 are backward compatible
- Follow these best practices

