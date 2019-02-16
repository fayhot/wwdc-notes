
## [Test Execution Speed](4-test-execution-speed.md) | Stuart | 2835 | p146

- Slow tests hinder developer productivity
- Want tests to run fast
- Artificial delays should not be necessary with sufficient mocking


### Testing Delayed Actions - Without the delay

How to use

- Identify the “delay” technique (e.g. Timer, DispatchQueue.asyncAfter)
- Mock this mechanism during tests
- Invoke delayed action immediately


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


