

## [Query Generations](1-query-generations.md) | | 125 | 

Some problems are challenging

### Faults in Core Data - Faults are tricksy things

- Managed objects
- Relationships
- Batch fetching result array

### Faults in Pictures

Faults
A rose by any other name
Futures Promises Lazy loading

### Why Faults? - Zero work is optimally efficient in some cases

- Avoid I/O
- Avoid CPU usage
- Avoid memory consumption
- What happens when row data is deleted?
  - (Oops, did I need that after all?)

### Handling Deletions

Current state of affairs

- managedObjectContext.shouldDeleteInaccessibleFaults
- Prefetch everything
  - Extra I/O, CPU, memory
- Write lots of code

### Stepping Back

User viewing UI doesn’t care

- Stability over immediacy
- Deferred/batched UI updates


User saving data doesn’t care
This is why we have merge policies


- What if ... ?
  - Provide UI with stable data?
  - Handle changes deterministically?

### Solution: Query Generations - We can be tricksier

- All reads from a context see a single generation of data
- Advance at predictable times
- Never see “could not fulfill a fault”
- Efficiently

### For Visual Learners

### Benefits

- Transactionality at context level
- Isolation of work in peer contexts
- Minimize speculative/preventative prefetching
- Everyone wins!


### The basics

Context chooses behavior

- Unpinned (current, default)
- Pin when data first loaded
- Pin to specific generation

Nested contexts always unpinned

- Inherit data from parent

### Changing Generations

- When explicitly updated
- On save
  - Linear stream of changes
- During `managedObjectContext.mergeChanges()`
- As a result of `managedObjectContext.reset()`

### Answers - To questions you haven’t thought to ask yet

Registered objects not refreshed on generation update

- managedObjectContext.fetch()
- managedObjectContext.refreshAllObjects()

You have control

### Requirements

- SQL store
- WAL mode
- Fails gracefully
  - Non-SQL stores have a single “TOT” generation


### Nuts and bolts: API

Opaque token to track generation

- New class NSQueryGenerationToken
- NSQueryGenerationToken.current()

Methods on NSManagedObjectContext that use it

- managedObjectContext.queryGenerationToken
- managedObjectContext.setQueryGenerationFrom()

### Nuts and bolts: Corners

Generation will not include stores added after token creation

- No results from stores not in generation 

Does not prevent you from removing stores from coordinator

- Error if no stores from generation remain