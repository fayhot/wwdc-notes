

## [GCD Design Patterns with QoS](2-gcd-design-patterns-with-qos.md) | Daniel A. Steffen | x | p46



QoS Propagation - Inferred QoS


- QoS captured at the time of Block submission
  - User Interactive translated to User Initiated
- Used if destination does not have QoS specified
  - Does not lower QoS


### Long-Running Job | p62-70


### Block QoS

- Block created with explicit QoS attribute
  - When work of another class is generated
- Captured at Block object creation
  - DISPATCH_BLOCK_ASSIGN_CURRENT
  - Store a callback Block for later submission


### Maintenance Task | p73-86



### Asynchronous Priority Inversion

- High QoS Block submitted to serial queue
  - Queue already contains Blocks with lower QoS
- Qos is raised until high QoS Block is reached  
  - Invisible to Blocks themselves


### Queue QoS - Recap
- Queues that are single purpose
  - Detached Blocks may also be appropriate
- Ignore QoS in asynchronous Blocks
  - Exceptional cases can enforce Block QoS


### Queues as Locks | p91-95


### Synchronous Priority Inversion

- High QoS thread waiting on lower QoS work
- QoS of waited on work is raised for
  - dispatch_sync() and dispatch_block_wait() of Blocks on serial queues 
  - pthread_mutex_lock()



