
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
1 Parallelism and concurrency|
[Concurrency](1-concurrency.md) | Daniel Chimene | 755 | p29
2 [Using GCD for Concurrency](2-using-gcd-for-concurrency.md) | Daniel A. Steffen | 1725 | p79
3 [Introducing Unified Queue Identity](3-introducing-unified-queue-identity.md) | Pierre Habouzit | 3040 | p154
4 [Modernizing Existing Code](4-modernizing-existing-code.md) | Pierre Habouzit | 4025 | p199


## 1 Parallelism and concurrency

Concept|Description|Cores
---|---|---
Parallelism|Simultaneous execution of closely related computations|multiple cores
Concurrency|Composition of independently executed tasks|even one core


### Take Advantage of System Frameworks

Accelerate / Metal 2 / Core ML / Core Animation


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
DispatchQueue.concurrentPerform(1000) { i in /* iteration i */

}
```

Parallelism

- Leverage system frameworks
- Use DispatchQueue.concurrentPerform
- Consider dynamic availability

