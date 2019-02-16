# [2015 406 UI Testing in Xcode](https://developer.apple.com/videos/play/wwdc2015/406)


- Wil Turner, Developer Tools
- Brooke Callahan, Developer Tools

TOC


Topic|Speaker|Time|Page
---|---|---|---
1 UI testing |
Demo| Brooke | 600 | P59
Find and interact with UI elements|
Validate UI properties and state|
2 UI recording|
Demo 2| Brooke | 2815 | p195
[3 Test Reports](3-test-reports.md) | Wil | 4400 | p201

### Core Technologies

- XCTest
- Accessibility

### Accessibility

- Rich semantic data about UI
- UIKit and AppKit integration
- APIs for fine tuning
- UI tests interact with the app the way a user does

### Requirements

- UI testing depends on new OS features
  - iOS 9
  - OS X 10.11
- Privacy protection
  - iOS devices
    - Enabled for development
    - Connected to a trusted host running Xcode
  - OS X must grant permission to Xcode Helper
    - Prompted on first run

Getting Started

- Xcode target type
- APIs
- UI recording



APIs

Three new classes

- XCUIApplication
- XCUIElement
- XCUIElementQuery

x

- UI Recording
- Interact with your app
- Recording generates the code
- Create new tests Expand existing tests


## Demo| Brooke | 600 | P59

Getting started with UI testing



## What Did You See? | 1205 |

- Adding a UI testing target
- Using recording
  - Finding UI elements
  - Synthesizing user events
- Adding validation with XCTAssert




### Example

```swift
Testing the Add button
// application:
let app = XCUIApplication()
app.launch()
// element and query:
let addButton = app.buttons[“Add”]
addButton.tap()
// assertion:
XCTAssertEqual(app.tables.cells.count, 1)
```

### See [1-1-api.md](1-1-api.md)

## Accessibility and UI Testing | | 2535 | p178

Debugging tips

- Not accessible
  - Custom view subclasses
  - Layers, sprites, and other graphics objects
- Poor accessibility data
- Tools
  - UI recording
  - Accessibility inspectors


## Demo 2| Brooke | 2815 | p195


### What Did You See? | Wil | 4250 | 

- Advanced UI testing
- Correcting queries
- Looping over elements
- Improving accessibility



## Ref

[User Interface Tests](https://developer.apple.com/documentation/xctest/user_interface_tests)

https://useyourloaf.com/assets/docs/UITestingCheatSheet.pdf
