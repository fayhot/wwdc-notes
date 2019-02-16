
## [Modernizing Existing Code](4-modernizing-existing-code.md) | | 4025 | p199


No dispatch object mutation after activation 

Protect your target queue hierarchy



### No Mutation Past Activation

Set the properties of inactive objects before activation

- Source handlers
- Target queues

```swift
let mySource = DispatchSource.makeReadSource(fileDescriptor: fd, queue: myQueue)
mySource.setEventHandler(qos: .userInteractive) { ... }
mySource.setCancelHandler { close(fd) }
mySource.activate()
mySource.setTarget(queue: otherQueue)
```

### Effects of Queue Graph Mutation

- Priority and ownership snapshots can become stale
  - Defeats priority inversion avoidance
  - Defeats direct handoff optimization
  - Defeats event delivery optimization
- System frameworks may create sources on your behalf
  - XPC connections are like sources


### Protecting the Target Queue Hierarchy

- Build your queue hierarchy bottom to top
- Opt into “static queue hierarchy”


```swift
Q1 = dispatch_queue_create("Q1", DISPATCH_QUEUE_SERIAL)
dispatch_set_target_queue(Q1, EQ)
 
Q1 = dispatch_queue_create_with_target("Q1", DISPATCH_QUEUE_SERIAL, EQ)
```


### Demo - Finding problem spots | Daniel A. Steffen 


