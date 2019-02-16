

# [2016 720 Concurrent Programming With GCD in Swift 3](https://developer.apple.com/videos/play/wwdc2016/720/)

dispatch/2016-720-concurrent-programming-with-gdc-in-swift-3/readme.md


- Matt Wright Darwin Runtime Engineer
- Pierre Habouzit Darwin Runtime Engineer





Concurrency

- Threads allow execution of code at the same time
- CPU cores can each execute a single thread at any given time
- Maintaining code invariants is more difficult with concurrency



Dispatch Queues and Run Loops

Asynchronous Execution


Synchronous Execution


Getting Work Off Your Main Thread


- Create a Dispatch Queue to which you submit work
- Dispatch Queues execute work items in FIFO order 
- Use `.async` to execute your work on the queue


```swift
let queue = DispatchQueue(label: "com.example.imagetransform")
queue.async {
    let smallImage = image.resize(to: rect)
    DispatchQueue.main.async {
        imageView.image = smallImage
    }
}
```


Controlling Concurrency
Thread pool will limit concurrency
Worker threads that block can cause more to spawn Choosing the right number of queues to use is important


## Structuring Your Application | | 820 | p67



- Identify areas of data flow in your application
- Split into distinct subsystems
- Queues at subsystem granularity


### Chaining vs. Grouping Work

### Grouping Work Together


```swift
let group = DispatchGroup()



group.notify(queue: DispatchQueue.main) { ... }
```



### Dispatch Inside Subsystems | | 1230 | p96


### Choosing a Quality of Service

- QoS provides explicit classification of work
- Indicates developer intent
- Affects execution properties of your work


### Using Quality of Service Classes

- Use `.async` to submit work with a specific QoS class
- Dispatch helps resolve priority inversions
- Create single-purpose queues with a specific QoS class

```swift
queue.async(qos: .background) {
    print("Maintenance work")
}
queue.async(qos: .userInitiated) {
    print(“Button tapped”)
}
```

### DispatchWorkItem


- By default .async captures execution context at time of submission
- Create DispatchWorkItem from closures to control execution properties
- Use .assignCurrentContext to capture current QoS at time of creation

```swift
let item = DispatchWorkItem(flags: .assignCurrentContext) {
    print("Hello WWDC 2016!")
}
queue.async(execute: item)
```

### Waiting for Work Items

- Use `.wait` on work items to signal that this item needs to execute
- Dispatch elevates priority of queued work ahead
- Waiting with a `DispatchWorkItem` gives ownership information
- Semaphores and Groups do not admit a concept of ownership

