
## [Using GCD for Concurrency](2-using-gcd-for-concurrency.md) | Daniel A. Steffen | 1725 | p79


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

- Serial queues and sources can form a tree
- Shared single mutual exclusion context
- Independent individual queue order


```swift
let Q1 = DispatchQueue(label: "Q1", target : EQ)
let Q2 = DispatchQueue(label: "Q2", target : EQ)
```

### Quality of Service

- Abstract notion of priority
- Provides explicit classification of your work
- Affects various execution properties


### QoS and Target Queue Hierarchy


## Granularity of Concurrency | 2435 | p119



### Event Monitoring Setup


Network Connection - Dispatch Source - Dispatch Queue

### Event Handling on Many Independent Queues



### Single Mutual Exclusion Context | p132

### Too Much of a Good Thing

- Repeatedly waiting for exclusive access to contended resources
- __Repeatedly switching between independent operations__
- Repeatedly bouncing an operation between threads


### Avoid Unbounded Concurrency -Repeatedly switching between independent operations 

Many workitems submitted to global concurrent queue

- If workitems block, more threads will be created
- May lead to thread explosion


### One Queue Hierarchy per Subsystem



### Good Granularity of Concurrency

- Fixed number of serial queue hierarchies
- Coarse workitem granularity between hierarchies
- Finer workitem granularity inside a hierarchy


### Using GCD for Concurrency

- Organize queues and sources into serial queue hierarchies 
- Use a fixed number of serial queue hierarchies
- Size your workitems appropriately