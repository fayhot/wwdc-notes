# [2017 414 Engineering for Testability](https://developer.apple.com/videos/play/wwdc2017/414)


2017-414-engineering-for-testability.md


Brian Croom, Xcode Engineer Greg Tracy, Xcode Engineer

• Testable app code
• Scalable test code

## Structure of a Unit Test

```swift
func testArraySorting() {
let input = [1, 7, 6, 3, 10]
let output = input.sorted() XCTAssertEqual(output, [1, 3, 6, 7, 10])
}
```


- Prepare input
- Run the code being tested
- Verify output


### Characteristics of Testable Code

- Control over inputs
- Visibility into outputs
- No hidden state


Testability Techniques
- Protocols and parameterization
- Separating logic and effects


## Protocols and Parameterization | | p20


```swift
@IBAction func openTapped(_ sender: Any) {
    let mode: String
    switch segmentedControl.selectedSegmentIndex {
    case 0: mode = "view"
    case 1: mode = "edit"
    default : fatalError("Impossible case")
    }
    let url = URL(string: "myappscheme://open?id=\(document.identifier)&mode=\(mode)")!
    
    if UIApplication.shared.canOpenURL (url){
        UIApplication.shared.open(url, options: [:], completionHandler: nil)
    }else {
        handleURLError()
    } 
}
```


```swift
class DocumentOpener {
    enum OpenMode: String {
        case view
        case edit
    }

    func open(_ document: Document, mode: OpenMode) {
        let modeString = mode.rawValue
        let url = URL(string: "myappscheme://open?id=\(document.identifier)&mode=\(modeString)")!

        if UIApplication.shared.canOpenURL(url) {
            UIApplication.shared.open(url, options: [:], completionHandler: nil)

        } else {
            handleURLError()
        }
    }

    let application: UIApplication
    init(application: UIApplication = UIApplication.shared) {
        self.application = application
    }
}
```

```swift
func testDocumentOpenerWhenItCanOpen() {
let app = /* ??? */
let opener = DocumentOpener(application: app)
         
}

protocol URLOpening {
    func canOpenURL(_ url: URL) -> Bool
    func open(_ url: URL, options: [String: Any], completionHandler: ((Bool) -> Void)?)
}
 
extension UIApplication: URLOpening {
    // Nothing needed here!
}


```

### MockURLOpener

```swift
class MockURLOpener: URLOpening {
        
func canOpenURL(_ url: URL) -> Bool {
}
func open(_ url: URL,
  
}
options: [String: Any],
completionHandler: ((Bool) -> Void)?) {
}
```


### Protocols and Parameterization

- Reduce references to shared instances
- Accept parameterized input
- Introduce a protocol
- Create a testing implementation

## Separating Logic and Effects


### Separating Logic and Effects

- Extract algorithms
- Functional style with value types
- Thin layer on top to execute effects


### Testability Techniques

- Protocols and parameterization
- Separating logic and effects

