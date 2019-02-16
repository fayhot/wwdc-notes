

## [Introducing Unified Queue Identity](3-introducing-unified-queue-identity.md) | Pierre Habouzit, Core Darwin | 3040 | p154

3-introducing-unified-queue-identity.md


Mutual Exclusion Context
Deep dive


let EQ = DispatchQueue(label: "com.example.exclusion-context")



### Asynchronous workitems



### Synchronous workitems



### One Identity to Find Them All  ... and in the kernel bind them


### Too Much of a Good Thing

- Repeatedly waiting for exclusive access to contended resources
- Repeatedly switching between independent operations
- __Repeatedly bouncing an operation between threads__


### Without Unified Identity - In macOS Sierra and iOS 10


### Leveraging Ownership and Unified Identity



The runtime uses every possible hint to optimize behavior


