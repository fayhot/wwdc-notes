
# [2017 706 Modernizing Grand Central Dispatch Usage](https://developer.apple.com/videos/play/wwdc2017/706/)


* Daniel Chimene, Core Darwin
* Daniel A. Steffen, Core Darwin
* Pierre Habouzit, Core Darwin


- Parallelism and concurrency
- Using GCD for concurrency
- Unified Queue Identity
- Finding problem spots

Topic|Speaker|Time|Page
---|---|---|---
2 [Using GCD for Concurrency](2-using-gcd-for-concurrency.md) | Daniel A. Steffen | 
3 [Introducing Unified Queue Identity](3-introducing-unified-queue-identity.md) | Pierre Habouzit | 3040 | p154
4 [Modernizing Existing Code](4-modernizing-existing-code.md) | | 4025 | p199


* Parallelism
  * Simultaneous execution of closely related computations
* Concurrency
  * Composition of independently executed tasks


Take Advantage of System Frameworks

Accelerate Metal 2 Core ML Core Animation


### Parallelism with GCD

- Express explicit parallelism with DispatchQueue.concurrentPerform
- Parallel for-loop—calling thread participates in the computation
- More efficient than many asyncs to a concurrent queue

```swift
DispatchQueue.concurrentPerform(1000) { i in /* iteration i */ } // Swift

dispatch_apply(DISPATCH_APPLY_AUTO, 1000, ^(size_t i){ /* iteration i */ }) // Objective-C

// DISPATCH_APPLY_AUTO deploys back to macOS 10.9, iOS 7.0
```


Dynamic Resource Availability

Choosing an iteration count

```swift
DispatchQueue.concurrentPerform(1000) { i in /* iteration i */ }
```

Parallelism

- Leverage system frameworks
- Use DispatchQueue.concurrentPerform
- Consider dynamic availability


## Concurrency

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


### Lock Ownership | 1530 |  p73

- Ownership helps resolve priority inversion
- High priority waiter
- Low priority owner


### Optimizing Lock Contention

- Inefficient behaviors are often emergent properties
- Visualize your app’s behavior with Instruments
- Use the right lock for the job

