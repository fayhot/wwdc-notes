


### [`XCUIApplication`](https://developer.apple.com/documentation/xctest/xcuiapplication)

- Proxy for the tested application
  - Tests run in a separate process
- Launch
  - Always spawns a new process
  - Implicitly terminates any preexisting instance
- Starting point for finding elements

### [`XCUIElement`](https://developer.apple.com/documentation/xctest/xcuielement)

- Proxy for elements in application
-  Types
  - Button, Cell, Window, etc.
-Identifiers
  - Accessibility identifier, label, title, etc.
- Most elements are found by combining type and identifier

Element Hierarchy Application is the root of a tree of elements

### Element Uniqueness

- Every XCUIElement is backed by a query
- Query must resolve to exactly one match
  - No matches or multiple matches cause test failure 
  - Failure raised when element resolves query
- Exception
  - exists property


### Event Synthesis

- Simulate user interaction on elements
- APIs are platform-specific
- button.click() // OS X
- button.tap() // iOS
- textField.typeText(“Hello, World!”) // iOS & OS X

### [`XCUIElementQuery`](https://developer.apple.com/documentation/xctest/xcuielementquery)

API for specifying elements

- Queries resolve to collections of accessible elements
  - Number of matches:count
  - Specify by identifier: subscripting
  - Specify by index:elementAtIndex()


###  XCUIElementQuery

Filtering

- Element type
  - Button, table, menu, etc.
- Identifiers
  - Accessibility identifier, label, title, etc.
- Predicates 
  - Value, partial matching, etc.

