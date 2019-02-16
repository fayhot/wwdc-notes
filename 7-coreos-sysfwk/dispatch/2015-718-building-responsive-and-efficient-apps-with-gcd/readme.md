


2015-718-building-responsive-and-efficient-apps-with-gcd/readme.md

# [2015 718 Building Responsive and Efficient Apps with GCD](https://developer.apple.com/videos/play/wwdc2015/718/)



- Anthony J. Chivetta - Darwin Runtime Engineer
- Daniel A. Steffen - Darwin Runtime Engineer



Topic|Speaker|Time|Page
---|---|---|---
Quality of Service Introduction
[GCD Design Patterns with QoS](2-gcd-design-patterns-with-qos.md) | Daniel A. Steffen | x | p46
[Queues, Threads, and Run Loops](3-threads-queues-and-run-loops.md) | Anthony J. Chivetta | | p97
[GCD and Crash Reports](4-gdc-and-crash-reports.md) | | | 



### Handling Events Asynchronously


### Competing Threads

### Quality of Service Classes

Abbr|Name|Y|Z
---|---|---|---
UI |User Interactive|Main thread, animations|Is this work actively involved in updating the UI?
IN |User Initiated|Immediate results|Is this work required to continue user interaction?
UT |Utility|Long-running tasks|Is the user aware of the progress of this work?
BG |Background|Not user visible|Is the user unaware of this work? Not user visible


Background : Can this work be deferred to start at a better time?



## Summary

- An efficient and responsive application must be able to adopt to diverse environments
- QoS classes enable the system to manage resources appropriately
- Integrate QoS into your application and existing use of GCD
- Consider your app’s use of GCD and avoid thread explosion