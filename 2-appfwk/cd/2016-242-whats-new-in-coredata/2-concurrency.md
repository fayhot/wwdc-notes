

[Concurrency](2-concurrency.md) - Something is always new | | 1340 | 

### Current stuff

Actor model for NSManagedObjectContext 

- Use `perform()` , `performAndWait()`
- `confinementConcurrencyType` is deprecated

Actor model for NSPersistentStoreCoordinator

- Use `perform()` , `performAndWait()`

Coordinator serializes contexts’ requests

### And Now an Important Message

Why did stuff start breaking after I recompiled?

`-performBlockAndWait:` now has an autorelease pool

Watch your NSError **

Affects MRR

Link time check

### Current State of Affairs

### New Stuff - I thought concurrency was hard, then I refactored

SQL store can now handle multiple concurrent requests

- Multiple readers
- Single writer

Connection pool

## Moving the Lock Down

### What does this mean?

More responsive UI

- Fault/fetch while background work occurs

Simpler application architecture

- Less need for multiple stacks
- Fewer complicated handoffs
- Bonus: shared row cache means lower memory footprint


### Connection Pool - Nuts and bolts: API

On by default

- SQL stores only
- All coordinated stores must be SQL stores

New store option: NSPersistentStoreConnectionPoolMaxSizeKey

- Specify max pool size
- Set to 1 if you want serialized request handling

We reserve the right to adjust pool size

### Considerations - How does it affect your code?

Should* be transparent

Better performance overall under contention

Code simplification

* Timing changed. If you depended on it, you may notice.
