
## [Working with Notifications](2-working-with-notifications.md) | Stuart |  |p78




- Test that subject properly observes or posts a Notification
- Important to test notifications in isolation
- Isolation avoids unreliable or “flaky” tests


### Testing Notification Observers

- How to use
  - Create separate NotificationCenter, instead of .default
  - Pass to init() and store in a new property
  - Replace all uses of NotificationCenter.default with new property
- Limits scope of tests by avoiding external effects



### Testing Notification Posters


- How to validate that a subject posts a Notification? Use a separate 
- NotificationCenter again
- Use XCTNSNotificationExpectation
 
 
