
## [Concurrency](1-concurrency.md) | Daniel Chimene | 755 | p29

Composition of independently executed tasks

### Context switching

> 2016-??? System Trace in Depth 

Context Switching

### The power of concurrency

The OS can choose a new thread at any time



- A higher priority thread needs the CPU
- A thread finishes its current work
- Waiting to acquire a resource
- Waiting for an asynchronous request to complete


### Excessive Context Switching

Too much of a good thing

Repeatedly bouncing between contexts can become expensive
CPU runs less efficiently
There may be others ahead in line for CPU access


### Excessive Context Switching - Too much of a good thing


- Repeatedly waiting for exclusive access to contended resources
- Repeatedly switching between independent operations
- Repeatedly bouncing an operation between threads

Lock Contention
Visualization in Instruments

Lock Contention


Fair locks


Unfair locks

### Lock Contention - Use the right lock for the job

X|Unfair|Fair
---|---|---
Available types|os_unfair_lock|pthread_mutex_t, NSLock DispatchQueue.sync
Contended lock re-acquisition|Can steal the lock|Context switches to next waiter
Subject to waiter starvation|Yes|No


### Lock Ownership | 1530 |  p73

- Ownership helps resolve priority inversion
  - High priority waiter
  - Low priority owner



Single Owner|No Owner|Multiple Owners
---|---|---
Serial queues|dispatch_semaphore|Private concurrent queues
DispatchWorkItem.wait|dispatch_group| 
os_unfair_lock|pthread_cond, NSCondition
pthread_mutex, NSLock|Queue suspension

 



### Optimizing Lock Contention

- Inefficient behaviors are often emergent properties
- Visualize your app’s behavior with Instruments
- Use the right lock for the job

