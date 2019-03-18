# [2015 508 Audio Unit Extensions](https://developer.apple.com/videos/play/wwdc2015/508)

2015-508-audio-unit-extensions/readme.md

2015-508-audio-unit-extensions/readme.md

- Doug Wyatt, Core Audio Plumber


Audio Units

- Since OS X 10.0, iOS 2.0
- OS includes many units
  - I/O, mixers, effects, more
  - Used in higher-level API’s (e.g. media playback)
- 3rd-party plug-ins (OS X)


### Audio Unit Extensions

- Full plug-in model
- OS X and iOS
- App Extensions -> App Store!
- New API
 - Modern
 - Compatible


### Version 3 Audio Unit API

- v1: 2001
- v2: 2002
- v3: AUAudioUnit class
  - In AudioUnit.framework
  - Objective-C / Swift


### AVFoundation

class|brief|OS X|iOS
---|---|---|---
AVAudioUnitComponentManager|Locate Audio Unit components|10.10+|9.0+
AVAudioUnitComponent|An Audio Unit component|10.10+|9.0+
AVAudioUnit AVAudioUnitEffect etc.|Audio Unit instance, in AVAudioEngine|10.10+|8.0+

### Compatibility (macOS)

## Demo - Audio Unit Extension in Logic Pro


Logic Pro with AU Extension

