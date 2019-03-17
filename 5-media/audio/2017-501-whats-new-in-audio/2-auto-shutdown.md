2-auto-shutdown.md

## Auto Shutdown

- Hardware is stopped if running idle for a certain duration,   started dynamically when needed
- Safety net for conserving power
- Enforced behavior on watchOS, optional on other platforms
- [`isAutoShutdownEnabled`](https://developer.apple.com/documentation/avfoundation/avaudioengine/2879211-isautoshutdownenabled)



Completion Callbacks
NEW
 Existing buffer/file completion handlers called when the data has been consumed New completion handler and callback types


[`AVAudioPlayerNodeCompletionCallbackType`](https://developer.apple.com/documentation/avfoundation/AVAudioPlayerNodeCompletionCallbackType) 

- `.dataConsumed`
  - Data has been consumed, same as the existing completion handlers
  - The buffer can be recycled, more data can be scheduled
- `.dataRendered`
  - Data has been output by the player
  - Useful in manual rendering mode
  - Does not account for any downstream signal processing latency
- `.dataPlayedBack`
  - Buffer/file has finished playing
  - Applicable only when the engine is rendering to an audio device
  - Accounts for both (small) downstream signal processing latency and (possibly significant) audio playback device latency

```swift
player.scheduleFile(file, at: nil, completionCallbackType: .dataPlayedBack) { (callbackType) in
// file has finished playing from listener’s perspective
// notify to stop the engine and update UI
})
```

### Deprecation coming soon (2018) - AUGraph

