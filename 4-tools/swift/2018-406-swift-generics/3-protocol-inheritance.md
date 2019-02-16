
## [3. Protocol inheritance](3-protocol-inheritance.md) | Doug | 2045 | p59

### The Collection Protocol Is Not Enough

- Some collection algorithms need more than Collection provides:
  - lastIndex(where:) needs to walk backwards to be efficient
  - shuffle() needs to swap elements to work at all
- Some conforming types have these capabilities


### Protocol Inheritance: BidirectionalCollection

- Inheritance describes additional requirements for a subset of conforming types
  - SinglyLinkedList cannot conform to BidirectionalCollection

### Use Inheritance to Provide More-Specialized Algorithms

Fisher-Yates Shuffle