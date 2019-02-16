

3-object-lifecycle-in-a-concurrent-world.md





Object Lifecycle in a Concurrent World | | 2200 | p131





1. Single threaded setup
2. activate the concurrent state machine
3. invalidate the concurrent state machine
4. Single threaded deallocation

### Observer Pattern


```swift 
class BusyController: SubsystemObserving {
   // ...
}

protocol SubsystemObserving {
   func systemStarted(...)
    func systemDone(...)
}

```


### Setup
Setup
Activated
Invalidated
Deallocation

```swift  
class BusyController: SubsystemObserving {
init(...) { ... }
}
```


### Activation

```swift
class BusyController: SubsystemObserving {
    init(...) { ... }
    func activate() {
        DataTransform.sharedInstance.register(observer: self, queue: DispatchQueue.main)
    }
}
```

### Active State Machine

```swift 
class BusyController: SubsystemObserving {
   func systemStarted(...) { /* ... */ }
   func systemDone(...) { /* ... */ }
}
```


### Deallocation


Abandoned memory


Deadlocks

using weak reference on observers to BusyController


```swift
// Deadlocks on Serial Queues Assert
Application Specific Information:
BUG IN CLIENT OF LIBDISPATCH: dispatch_barrier_sync called on queue already owned by current
thread
Thread 1 Crashed:: Dispatch queue: com.example.queue
_dispatch_barrier_sync_f_slow
__main_block_invoke_2
_dispatch_client_callout
_dispatch_barrier_sync_f_invoke
__main_block_invoke
_dispatch_call_block_and_release
_dispatch_client_callout
_dispatch_queue_serial_drain
0   libdispatch.dylib
1 <YOUR APP>
2   libdispatch.dylib
3   libdispatch.dylib
4 <YOUR APP>
5   libdispatch.dylib
6   libdispatch.dylib
7   libdispatch.dylib
...
0x00007fff920b44ee
0x000000010a3d7f26
0x00007fff920a8ed6   +8 0x00007fff920a9b0e
0x000000010a3d7ef6
0x00007fff920b1d54
0x00007fff920a8ed6   +8 0x00007fff920c2d34
```

### Explicit Invalidation

```swift
class BusyController: SubsystemObserving {

    func invalidate() {
        dispatchPrecondition(.onQueue(DispatchQueue.main))
        DataTransform.sharedInstance.unregister(observer: self)
    }
    deinit { }
}
```

### Invalidation as a State

```swift
class BusyController: SubsystemObserving {
    private var invalidated: Bool = false
    func systemStarted(...) {
        if invalidated { return }
        /* ... */
    }
    deinit {
        precondition(invalidated)
    } 
}
```

### GCD Object Lifecycle | | 3030 | p168


### Setup

Attributes and target queue Source handlers

```swift
  let q = DispatchQueue(label: "com.example.queue", attributes: [.autoreleaseWorkItem])
let source = DispatchSource.read(fileDescriptor: fd, queue: q)
source.setEventHandler { /* handle your event here */ }
source.setCancelHandler { close(fd) }
```


### Activation
 
Properties of dispatch objects must not be mutated after activation

Queues can also be created inactive

```swift
extension DispatchObject {
   func activate()
}
let queue = DispatchQueue(label: “com.example.queue”, attributes: [.initiallyInactive])
 
```


### Cancellation

Sources require explicit cancellation

- Event monitoring is stopped
- Cancellation handler runs
- All handlers are deallocated


```swift
let source = DispatchSource.read(fileDescriptor: fd, queue: q)
source.setCancelHandler { close(fd) }
```

### Deallocation Hygiene

GCD Objects expect to be in a defined state at deallocation
- Activated
- Not suspended