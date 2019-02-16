## [Exclusive access to memory - John McCall, Swift Compiler Team](402-4-exclusive-access-to-memory.md)


### Ownership

* Make it easier to reason about local variables
* Enable better programmer optimization
* Enable better compiler optimization
* Enable powerful new language features


```swift

var numbers = [1, 2, 3] numbers.modifyEach { element in
    element *= 2
    numbers.removeLast()
}
// numbers == ???

```

### Non-Exclusive Access to Memory

* Hard to reason about
* Creates corner cases
* Performance problems for libraries
* Performance problems for the compiler


### SE-0176: Enforcing Exclusive Access to Memory


### Run-time Enforcement

* Global variables
* Properties of classes
* Local variables captured in escaping closures




## Exclusive Access to Memory
John McCall, Swift Compiler Team


```
Non-Exclusive Access to Memory
Hard to reason about
Creates corner cases
Performance problems for libraries Performance problems for the compiler
```

Run-time Enforcement
Global variables
Properties of classes
Local variables captured in escaping closures


### Taking Advantage of Exclusive Access

* More reliable performance Lots of optimization
* In libraries
* In the compiler In your code
* New language opportunities
* https://github.com/apple/swift/blob/master/docs/OwnershipManifesto.md
