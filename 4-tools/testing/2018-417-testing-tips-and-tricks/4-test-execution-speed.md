
## [Test execution speed](4-test-execution-speed.md) | | p146

Test Execution Speed

- Slow tests hinder developer productivity
- Want tests to run fast
- Artificial delays should not be necessary with sufficient mocking


```swift
class FeaturedPlaceManager {
    var currentPlace: Place
    func scheduleNextPlace() {
        // Show next place after 10 seconds
        Timer.scheduledTimer(withTimeInterval: 10, repeats: false) { [weak self] _ in
            self?.showNextPlace()
        }
    }
    func showNextPlace() {
        // Set currentPlace to next place...
    } 
}
```

```swift
class FeaturedPlaceManagerTests: XCTestCase {
    func testScheduleNextPlace() {
        let manager = FeaturedPlaceManager()
        let beforePlace = manager.currentPlace
        manager.scheduleNextPlace() 
        
        //   Slow! Not ideal
        RunLoop.current.run(until: Date(timeIntervalSinceNow: 11))

        // Less slow but still timing-dependent
        RunLoop.current.run(until: Date(timeIntervalSinceNow: 2))

        XCTAssertNotEqual(manager.currentPlace, beforePlace)
    } 
}
```

### Testing Delayed Actions | | p152
Without the delay 

How to use

- Identify the “delay” technique (e.g. Timer, DispatchQueue.asyncAfter)
- Mock this mechanism during tests
- Invoke delayed action immediately

```swift
class FeaturedPlaceManagerTests: XCTestCase {
    func testScheduleNextPlace() {
        var timerScheduler = MockTimerScheduler()
        var timerDelay = TimeInterval(0)
        timerScheduler.handleAddTimer = { timer in
            timerDelay = timer.fireDate.timeIntervalSinceNow
            timer.fire()
        }
        let manager = FeaturedPlaceManager(timerScheduler: timerScheduler)
        let beforePlace = manager.currentPlace
        manager.scheduleNextPlace()
//       No delay!
        XCTAssertEqual(timerDelay, 10, accuracy: 1)
        XCTAssertNotEqual(manager.currentPlace, beforePlace)
    }
```

### Testing Delayed Actions

- Delay is eliminated using this technique
- Majority of tests should be direct, without mocking delays


### Setting Expectations

- Be mindful when using XCTNSPredicateExpectation
- Slower and best suited for UI tests
- Use faster, callback-based expectations in unit tests:
  - XCTestExpectation
  - XCTNSNotificationExpectation
  - XCTKVOExpectation

### Optimizing App Launch When Testing

- Avoid unnecessary work when app is launched as unit test host
- Testing begins after ‘app did finish launching’
- Set custom scheme environment variables/launch arguments for testing  

