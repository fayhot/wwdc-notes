

## The design of SwiftPM | 1230 | p50

Following Swift’s Philosophy

- Safe: isolated build environment
- Fast: scalable to large dependency graphs
- Expressive: Swift language manifest format



TOC

- Configuration
- Dependencies
- Workflow  Features
- Building
- Tools Evolution

## 1 Configuration

### Swift Language Manifest Format

- Easy to understand
- Follows Swift API design guidelines
- Supported by existing Swift tools

### Prefer Declarative Syntax

### Specifying Package Source Files


### Convention versus Configuration


### Support for Building Other Languages


## 2 Dependencies


Semantic Versioning

semver.org

Version|Y
---|---
Major Version|Breaking changes
Minor Version|Compatible additions
Patch Version|Bug fixes



### Dependency Resolution

### Direct Dependencies

### Resolving Versions

### Transitive Dependencies

### Resolving Products

### Package.resolved Resolved Versions File

- Records resolved package versions
- Can be shared for dependable build results 
- Easy to update with new version resolution 
- Only used from the top-level package

## 3 Building


### llbuild

- SwiftPM’s build execution engine
- Provides fast and correct incremental builds
- Also used by Xcode’s new build system 
- Part of the Swift open source project


### Build Environment Isolation

- SwiftPM builds packages in isolation
- Builds are sandboxed
- No arbitrary commands or shell scripts

### Testing

### Parallel Testing


### Test Filtering

## 4 Workflow Features



### Edit Mode

### Branch Dependencies

### Local Package Dependencies


## 5 Tools Evolution

### Package.swift Manifest API Evolution

- Package API can be updated with each new Swift version
- Previous API is still available
- Allows using new Swift tools without updating the manifest


### Swift Tools Version

```swift
// swift-tools-version:4.2
import PackageDescription
let package = Package(..., swiftLanguageVersions: [.v4_2, .v4])
```