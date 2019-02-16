

416-swift-performance


dimensions


 X | Y
 --|--
Allocation | Stack – Heap
Reference Counting | Less – More
Method Dispatch |  Static  - Dynamic ; Compile-time – Runtime


## stack – heap

decrement stack pointer to allocate
increment stack pointer to deallocate

X | structs | class
--|--|--
allocated in |stack |heap
Characteristics | | identity and indirect storage

Unintented sharing of state.


3 enums

struct Attributes : Hashable {


### Heap + Reference Counting

Retain and release by ARC




Method Dispatch

Compiler visibility

No stack overhead


Take aways, from




Protocol type = keep your code polymorphic , and away from class-subclass

The existential container
Boxing values of protocol types

X | Description | Length
--|--|--
valueBuffer |Inline value buffer |current 3 words
Vwt | Reference to Value Witness Table
Pwt |Reference to Protocol Witness Table



Value Witness Table (VWT)

Allocation, copy, destruction of any value

Allocate:
Copy:
Destruct :
Deallocate :

PWT

Draw:



Specialization of Generics

Static polymorphism: uses type at call-site
Creates type-specific version of method
Version per type in use
Can be more compact after optimization




When

Whole module optimization – increase optimization opportunity






Unspecialized Generics – Large Value

Heap allocation (use indirect storage as a workaround)
Reference counting if value contains references
Dynamic dispatch through protocol Witness Table

=-====

Summary/Take-away

Choose fitting abstraction with the least dynamic runtime type requirements
	Struct types: value semantics
	Class types; identity or OOP style polymorphism
	Generics : static polymorphism
	Protocol types: dynamic polymorphism
Use indirect storage to deal with large values
