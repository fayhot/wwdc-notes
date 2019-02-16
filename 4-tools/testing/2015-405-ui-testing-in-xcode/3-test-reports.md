
## [Test Reports](3-test-reports.md) | Wil | 4400 | p201

UI Refresh


- Show results for all tests
  - Pass/fail
  - Failure reason
  - Performance metrics
- Same UI in Xcode and in Xcode Server
- Per-device results for Xcode Server


UI testing additions

- New data
- Screenshots
- Nested activities

Nested activities

- UI testing APIs have several steps
- Typing into a textfield
  - Wait for the app to idle
  - Evaluate the textfield query
  - Synthesize the text input
  - Wait for the app to idle
- QuickLook for screenshots

When to Use UI Testing

Using UI Testing

- Complements unit testing
- Unit testing more precisely pinpoints failures
- UI testing covers broader aspects of functionality
- Find the right blend of UI tests and unit tests for your project

Candidates for UI Testing

- Demo sequences
- Common workflows
- Custom views
- Document creation, saving, and opening

