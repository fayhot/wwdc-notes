## [Tools and performance - Bob Wilson, Swift Performance Team](402-2-tools-and-performance.md) (11~)


### New Build System

Xcode 9 includes a preview of a new build system

Fast: lower overhead, especially for large projects


### Precompiled Bridging Headers
Bridging header for large mixed-source projects can be slow to parse

Speeds up Apple’s Music app build by 40%

### Shared Build for Coverage Testing


Xcode 8 builds separately for coverage testing Coverage instrumentation is very low overhead
Xcode 9 shares the same build → avoid building twice

### Indexing While Building

* Background indexing often duplicates effort
* Build process now updates the index
* More accurate results

### Predictable Performance - Runtime

```swift
// Unpredictable Performance in Swift 3
protocol Ordered {
   func precedes(_ other: Ordered) -> Bool
}
func testSort(_ values: inout [Ordered]) {
   values.sort { $0.precedes($1) }
}
```

2016


###


### Existential Containers

* Implementation of a value of unknown type
* Inline value buffer: currently three words
* Large values stored on the heap
* Heap allocation is slow


#### COW Existential Buffers

* Swift now uses copy-on-write (COW) reference-counted existential buffers
* Copied only when modified while not uniquely referenced
* Avoids expensive heap allocations


#### Faster Generic Code

* Specialization: compiler generates code for specific types
* Not always possible: unspecialized generic code is also important
* Stack allocation of generic buffers


### Smaller Binaries


```swift
// Unused Conformance Removal
struct Date {
private let secondsSinceReferenceDate: Double
}
extension Date: Equatable {
static func ==(lhs: Date, rhs: Date) -> Bool {
return lhs.secondsSinceReferenceDate == rhs.secondsSinceReferenceDate
}
}
extension Date: Comparable {
static func <(lhs: Date, rhs: Date) -> Bool {
return lhs.secondsSinceReferenceDate < rhs.secondsSinceReferenceDate
}
}
```

### Unused \@objc Thunks


### SE-0160: Limited \@objc Inference

* Swift 4 only infers \@objc when it is needed
  * Overriding an Objective-C method
  * Conforming to an Objective-C protocol
* Reduced size of Apple’s Music app by 5.7%


### Migration for Minimal Inference

* Migrator cannot identify all the functions that need \@objc
* Inferred Objective-C thunks marked as deprecated to help you find them
  * Build warnings about deprecated methods
  * Console messages when running deprecated thunks


#### Finish Migration
Change build setting to Default
Apple’s Music app migration: only a handful of manual changes required


### Symbol Size

* Swift symbols take up a lot of space
* Example: macOS libswiftCore library



#### Symbol Stripping

* Swift standard libraries are stripped during App Thinning 
* New option when exporting project archive
