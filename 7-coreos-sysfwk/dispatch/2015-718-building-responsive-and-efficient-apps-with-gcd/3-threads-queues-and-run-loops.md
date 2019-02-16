
## [Queues, Threads, and Run Loops](3-threads-queues-and-run-loops.md) | Anthony J. Chivetta | | p97


Run Loop Versus Queue
dispatch_async(q, ^{
 [self performSelector:@selector(thing) withObject:nil afterDelay:1];
});



### Properties

X| Run Loop | Serial Queue
---|---|---
•|Bound to a thread|Uses ephemeral threads
•|Gets delegate method callbacks|Block callbacks
•|Autorelease pool pops after each iteration|Autorelease pool pops when thread idle 
•|Can be used reentrantly|Will deadlock if used reentrantly



 
The Main Thread’s Run Loop is also exposed as the Main Queue


RunLoop Versus Queue
### Timer APIs

```
RunLoop
-[NSObject performSelector:withObject:afterDelay:]
+[NSTimer scheduledTimerWithTimeInterval:]
Queue
dispatch_after()
dispatch_source_set_timer()
```

### Thread Creation and Pooling


Waiting

A thread waits (blocks) when it needs to wait for a resource such as I/O or locks When a thread waits, GCD may spin up a new thread to ensure one thread per core


### Thread Creation and Waiting


### Thread Explosion


Thread Explosion Causing Deadlock


Avoiding Thread Explosion
Always good advice: use asynchronous APIs, especially for I/O
Use serial queues
Use NSOperationQueues with concurrency limits
    NSOperationQueue.maxConcurrentOperationCount
Don’t generate unlimited work...



### Avoiding Thread Explosion - Mixing sync and async


```swift
// fast, just a lock
dispatch_sync(q, ^{...});
// fast, just an atomic enqueue
dispatch_async(q, ^{...});
// slow, has to wait far a thread to complete above Block
dispatch_sync(q, ^{...});
```

Be super careful about mixing these from the main thread!


### Avoiding Thread Explosion - dispatch_apply


```swift
// DANGEROUS – may cause thread explosion and deadlocks
for (int i = 0; i < 999; i++){
    dispatch_async(q, ^{...});
}
dispatch_barrier_sync(q, ^{});
// GOOD – GCD will manage parallelism
dispatch_apply(999, q, ^(size_t i){...});
```

### Avoiding Thread Explosion - dispatch_semaphore

```c
#define CONCURRENT_TASKS 4

sema = dispatch_semaphore_create(CONCURRENT_TASKS);
for (int i = 0; i < 999; i++){
    dispatch_async(q, ^{
        // do work
        dispatch_semaphore_signal(sema);
    });
    dispatch_semaphore_wait(sema, DISPATCH_TIME_FOREVER);
}
```

