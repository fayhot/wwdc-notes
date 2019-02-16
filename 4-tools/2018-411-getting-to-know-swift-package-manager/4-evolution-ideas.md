## Evolution ideas

Open Evolution Process

### Themes

- Great integration with other tools
- Publish and deploy
- Support complex packages
- Find, manage, and trust packages


## Great Integration with Other Tools


### libSwiftPM Available


### SwiftPM support in  developer tools is encouraged!


### Idea: Machine-Editable Package.swift

```swift
let package = Package(
    name: "Networking", 
    products: [
        .library(name: "Networking", targets: ["Networking"]
    ],
    targets: [
      .target(
          name: "Networking", dependencies: []),
    ] 
)
 
```

## Publish and Deploy



### Idea: Tagging and Publication Support

### Idea: Automatic Semantic Versioning

### Idea: Deployment Automation


## Support Complex Packages

### Idea: Resources

### Idea: Build Settings

### Idea: Extensible Build Tools


## Trust, Manage, and Find Packages


### Idea: Package Content Verification


### Idea: Cross-Platform Sandboxing

### Idea: Fork Support

### Idea: Package Index


## Your Contributions


# • Open source process p124


https://swift.org/package-manager/



https://github.com/apple/swift-evolution

https://forums.swift.org/c/development/SwiftPM

https://bugs.swift.org


@swift-ci please test


https://swift.org/download/#snapshots

Growing Community

Server-Side Swift

Command-Line Utilities

$ swift package init

# The End