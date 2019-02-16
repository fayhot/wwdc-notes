
## [Test Concepts](1-test-concepts.md) | | p33


Testing Timeline 

- Compilation
- Hosting
- Observation


### Test Hosting

#### How testing starts



#### Comparison

X|Unit Tests|UI Tests
---|---|---
X|Direct access to host app data and APIs|Uses Accessibility to access target app
X|All tests run in single app launch|Tests launch app for every test case



### Test Observation

#### Test case structure

- Setup or tear down work
- Custom logging


#### XCTestObservation Protocol

- optional public func testBundleWillStart(_ testBundle: AnyObject!)
- optional public func testSuiteWillStart(_ testSuite: AnyObject!)
- optional public func testCaseWillStart(_ testCase: AnyObject!)
- optional public func testCaseDidFinish(_ testCase: AnyObject!)
- optional public func testCase(_ testCase: AnyObject!, didFailWithDescription
   description: AnyObject!, inFile filePath: AnyObject!, atLine lineNumber: AnyObject!)
- optional public func testSuiteDidFinish(_ testSuite: AnyObject!)
- optional public func testBundleDidFinish(_ testBundle: AnyObject!)

#### Sample Code

```swift
// Test Observation
// Example LoggingObserver
class LoggingObserver: NSObject, XCTestObservation {
    override init() {
        super.init()
        let sharedCenter = XCTestObservationCenter.shared()
        sharedCenter.addTestObserver(self)
    }
    internal func testBundleWillStart(_ testBundle: Bundle) {
        print("Lights down, show is about to start")
    }
    internal func testCase(_ testCase: AnyObject!, didFailWithDescription
        description: AnyObject!, inFile filePath: AnyObject!, atLine lineNumber: AnyObject!)
        print("That sounds off key...")
    }
    internal func testBundleDidFinish(_ testBundle: Bundle) {
        print("Lights up, don’t forget your coat!")
    } 
}
```

#### Use NSPrincipalClass

- Test Bundle Info.plist
- Test specific instantiation