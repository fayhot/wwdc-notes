2014-716-power-performance-and-diagnostics-whats-new-in-gcd-and-xpc/readme.md


# [2014 716 Power, Performance and Diagnostics: What's new in GCD and XPC](https://developer.apple.com/videos/play/wwdc2014/716/)


Daniel Steffen


Background
Quality of Service Class

New QoS and GCD API
Propagation of QoS and Execution Context
Diagnostics and Queue Debugging

Asynchronous execution
Concurrent execution
Syncrhonization


Past Sessions


The Big Picture

Primary Goal

- Provide best user experience
- What is important to user?
  - Frontmost app
  - Responsive user interface

### Responsive user interface

Ensure resource availability for 

- Main thread of frontmost app
  - UI event handling
  - UI drawing
- OS User Interface infrastructure

Other work should execute

- Off main thread
- Independently
- At lower priority

Priorities

- Resolving resource contention
- Under contention 
  - High proirties win
- No contention
  - Low priorities have no restriction


## Choosing QoS Class


