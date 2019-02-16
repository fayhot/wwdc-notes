

# [2018 411 Getting to Know Swift Package Manager](https://developer.apple.com/videos/play/wwdc2018/411/)

- Rick Ballard, SwiftPM Release Manager 
- Boris Buegling, Developer Tools Engineer



2018-411-getting-to-know-swift-package-manager 


- Why a package manager for Swift?
- How to use it
- The design of SwiftPM
- Evolution ideas
- Open source process


## A Cross-Platform Build System for Swift


https://swift.org/package-manager/

https://swift.org/download/


## How to use it




```bash

$ swift build

$ swift run 

$ swift test 

$ swift package

```

•Demo
• Creating your first package

Anatomy of a Package

- Targets
- Dependencies
- Products


```swift
 // swift-tools-version:4.2
 import PackageDescription
let package = Package(
    name: "dealer",
    products: [
        .library(name: "libdealer", targets: ["libdealer"]),
        .executable(name: "dealer", targets: ["dealer"]),
    ],

    dependencies: [
        .package(url: "git@github.com:apple/example-package-deckofplayingcards", from: "3.0.0")
    ],
    targets: [
        .target(name: "libdealer", dependencies: ["DeckOfPlayingCards"]),
        .target(name: "dealer", dependencies: ["libdealer"]),
        .testTarget(name: "dealerTests", dependencies: ["libdealer", "dealer"]),
    ]
)
```
