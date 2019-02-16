
## [Working with Notifications](2-working-with-notifications.md) | | p72


Test that subject properly observes or posts a Notification Important to test notifications in isolation
Isolation avoids unreliable or “flaky” tests


```swift
class PointsOfInterestTableViewController {
    var observer: AnyObject?
    init() {
        let name = CurrentLocationProvider.authChangedNotification
        observer = NotificationCenter.default.addObserver(forName: name, object: nil,
            self?.handleAuthChanged()
        }
}
    var didHandleNotification = false
    func handleAuthChanged() {
        didHandleNotification = true
    }
}
```


```swift
class PointsOfInterestTableViewControllerTests: XCTestCase {
    func testNotification() {
        let observer = PointsOfInterestTableViewController()
        XCTAssertFalse(observer.didHandleNotification)
//   This notification will be received by all objects in process, // could have unintended consequences
let name = CurrentLocationProvider.authChangedNotification NotificationCenter.default.post(name: name, object: nil)
        XCTAssertTrue(observer.didHandleNotification)
    }
}
```


### Testing Notification Observers

- How to use
  - Create separate NotificationCenter, instead of .default
  - Pass to init() and store in a new property
  - Replace all uses of NotificationCenter.default with new property
- Limits scope of tests by avoiding external effects

```swift
class PointsOfInterestTableViewController {
    var observer: AnyObject?
init() {
        let name = CurrentLocationProvider.authChangedNotification
        observer = NotificationCenter.default.addObserver(forName: name, object: nil,
        self?.handleAuthChanged()
    }
}
var didHandleNotification = false
func handleAuthChanged() {
    didHandleNotification = true
}

```

```swift
class PointsOfInterestTableViewControllerTests: XCTestCase {
    func testNotification() {
        let observer = PointsOfInterestTableViewController()
        XCTAssertFalse(observer.didHandleNotification)
//   This notification will be received by all objects in process, // could have unintended consequences
let name = CurrentLocationProvider.authChangedNotification NotificationCenter.default.post(name: name, object: nil)
        XCTAssertTrue(observer.didHandleNotification)
    }
}
```

### Testing Notification Posters

- How to validate that a subject posts a Notification?
- Use a separate NotificationCenter again
- Use XCTNSNotificationExpectation
 
```swift
class CurrentLocationProvider {
    static let authChangedNotification = Notification.Name("AuthChanged")
    func notifyAuthChanged() {
        let name = CurrentLocationProvider.authChangedNotification
        NotificationCenter.default.post(name: name, object: self)
    } 
}
```

```swift
class CurrentLocationProviderTests: XCTestCase {
    func testNotifyAuthChanged() {
        let notificationCenter = NotificationCenter()
        let poster = CurrentLocationProvider(notificationCenter: notificationCenter)
        
        //       Notification only sent to this specific center, isolating test
        let name = CurrentLocationProvider.authChangedNotification
        let expectation = XCTNSNotificationExpectation(name: name, object: poster,
                                         notificationCenter: notificationCenter)
        poster.notifyAuthChanged()
        wait(for: [expectation], timeout: 0)
    }
}
```

