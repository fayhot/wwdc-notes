
# [2019 226 Data Flow Through SwiftUI](https://developer.apple.com//videos/play/wwdc2019/226/)



Principles of Data Flow

Anatomy of an Update

Understanding Your Data


Tools for Data Flow

@Environment @Binding @State Property BindableObject

Principle 1: Data Access as a Dependency

Principle 2: Sources of Truth

Duplicated Source of Truth - problem.. inconsistency - vs Single Source of Truth.



BindableObject

### Creating Dependencies on BindableObject

@ObjectBinding

### Indirect Dependencies

@EnvironmentObject


### Environment

- Data applicable to an entire hierarchy
- Convenience for indirection
- Accent color, right-to-left, and more


Sources of Truth

X|@State|BindableObject
---|---|---
x|View-Model|Extneral
x|Value|Reference
x|Framework Managed|Developer Managed

### Building Reuseable Components

Read-only: Swift property, Environment
: @Binding
: @State - Use derived Binding or value


Next Steps

- Minimze Source of Truth
- Understand your data
- Build a great app!