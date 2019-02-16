# [2018 605 2018 605 Inside SwiftShot: Creating an AR Game](https://developer.apple.com/videos/play/wwdc2018/605)


2018-605-inside-swiftshot-creating-an-ar-game/readme.md

```
• Designing Games for AR
• SwiftShot Internals
• World Map Sharing
• Networking
• Physics
• Wrap-up
```

Topic|Speaker|Time|Page
---|---|---|---
Designing Games for AR|
[Sharing a World Map](3-world-map-sharing.md) | | 11? | p41
[Networking with Multipeer Connectivity](4-networking.md) |||p63
Physics | | | p79


## Designing Games for AR | | t | p

Gameplay must come first

Designing Games for Augmented Reality

- Start with the gameplay
- Short sessions with easy engagement
- Variety of content to keep it fresh
- Spectating turned out to be interesting
- Social interaction and personal connection
- Consider the benefits of AR

Control Mechanisms

- Encourage slow movement of the device
- Encourage the player to move
- Control feedback is important for immersion


## SwiftShot Internals | David Paschich, Tools Foundation | 750 | p26

Techologies: ARKit, SceneKit, Metal, GameplayKit, PeerConnectivity, AVFoundation, Swift


SwiftShot Internals

- Establishing a shared coordinate space
- Networking and state sharing
- Physics
- Asset import and management
- Flag simulation
- Dynamic audio

### Establishing a Shared Coordinate Space

- Image detection
- Object detection
- World Map sharing
- iBeacons for fixed installations

## [Sharing a World Map](3-world-map-sharing.md) | | 11? | p41




## [Networking with Multipeer Connectivity](4-networking.md) |||p63


## Physics | | | p79

- SceneKit physics
- All peers run physics simulation
- “Server” sends updates to clients to ensure synchronization
- Only “game state” relevant information is shared
- Objects scaled approximately 10x for better performance


