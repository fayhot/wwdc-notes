2019-722-introducing-combine.md



A unified, declarative API for   processing values over time


Combine Features

Generic / Type safe / Composition first / Request driven

Key Concepts

Publishers / Subscribers / Operators


Publisher

- Defines how values and errors are produced
- Value type
- Allows registration of a Subscriber


Subscriber
Receives values and a completion Reference type


The Pattern

- Subscriber is attached to Publisher
- Publisher sends a Subscription
- Subscriber requests N values
- Publisher sends N values or less
- Publisher sends completion

Operator


- Adopts Publisher
- Describes a behavior for changing values
- Subscribes to a Publisher (“upstream”)
- Sends result to a Subscriber (“downstream”)
- Value type


Declarative Operator API

- Functional transformations
- List operations
- Error handling
- Thread or queue movement
- Scheduling and time


X|Synchronous|Asynchronous
--|--|--
One|Int|Future
Many|Array|Publisher

## Combining Publishers

- Zip
- CombineLatest



Zip

- Converts several inputs into a single tuple
- A “when/and” operation
- Requires input from all to proceed


Combine Latest

- Converts several inputs into a single value
- A “when/or” operation
- Requires input from any to proceed
- Stores last value


Try It

- Process a NotificationCenter post with filter
- Await completion of two network requests with zip
- decode the data of a URLResponse


More to Combine

- Error handling and cancellation
- Schedulers and time
- Design patterns