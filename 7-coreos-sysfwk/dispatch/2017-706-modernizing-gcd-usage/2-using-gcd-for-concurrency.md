
## [Using GCD for Concurrency](2-using-gcd-for-concurrency.md) | Daniel A. Steffen | 


```swift
let queue = DispatchQueue(label: "com.example.queue") 
queue.async { /* 1 */ }
queue.async { /* 2 */ }
queue.sync  { /* 3 */ }
```


### Dispatch Source

Event monitoring primitive

```swift 
let source = DispatchSource.makeReadSource(fileDescriptor: fd, queue: queue) 
source.setEventHandler { read(fd) }
source.setCancelHandler { close(fd) }
source.activate()
```


### Target Queue Hierarchy

Serial queues and sources can form a tree



### Quality of Service

- Abstract notion of priority
- Provides explicit classification of your work
- Affects various execution properties


## Granularity of Concurrency | 2435 | p119



Event Monitoring Setup


Network Connection - Dispatch Source - Dispatch Queue

