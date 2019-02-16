

2-shared-state-synchronization.md



## Shared State Synchronization |  Pierre Habouzit Darwin Runtime Engineer | 1620 | p114 


### Swift 3 and Synchronization - Synchronization is not part of the language in Swift 3

- Global variables are initialized atomically
- Class properties are not atomic
- Lazy properties are not initialized atomically

### “There is no such thing as a benign race.”

Herb Sutter Chair of the ISO C++ standards committee


> Thread Sanitizer and Static Analysis


### Correct Use of Traditional Locks

- Foundation.Lock can be used safely because it is a class
- Derive an Objective-C base class with struct based locks as ivars

```objc
@implementation LockableObject {
   os_unfair_lock _lock;
}
- (instancetype)init ...
- (void)lock   { os_unfair_lock_lock(&_lock); }
- (void)unlock { os_unfair_lock_unlock(&_lock); }
@end
```

### Use GCD for Synchronization

- Use DispatchQueue.sync(execute:)
  - harder to misuse than traditional locks, more robust
  - better instrumentation (Xcode, assertions, ...)


```swift
// Use Explicit Synchronization
   
class MyObject {
    private let internalState: Int
    private let internalQueue: DispatchQueue
    var state: Int {
        get {
            return internalQueue.sync { internalState }
        }
        set (newState) {
            internalQueue.sync { internalState = newState }
        }
    }
}
```

### Preconditions - Avoid data corruption

- GCD lets you express several preconditions
  - Code is running on a given queue
  - Code is not running on a given queue


```swift
dispatchPrecondition(.onQueue(expectedQueue)))
dispatchPrecondition(.notOnQueue(unexpectedQueue)))
```
