

# [2016 509 Speech Recognition API](https://developer.apple.com/videos/play/wwdc2016/509/)

2016-509-speech-recognition-api.md

Understanding what your users say 

- Henry Mason Siri Speech



## Speech Recognition

What is it?

- Highly accurate
- State of the art
- Easy to use
- Fast
- Many languages
- Respects user privacy



## Using Speech Recognition

Explain, authorize, request

- Explain why in your Info.plist
If your app “Phromage” would like to access Speech Recognition...
Usage Description— This will allow you to take a photo just by saying “cheese.”

- Request authorization using SFSpeechRecognizer.requestAuthorization

- Create recognition request
• Pre-recorded on disk, use SFSpeechURLRecognitionRequest
From live audio or memory, use SFSpeechAudioBufferRecognitionRequest Give Request to Recognizer
• Optionally hold onto SFSpeechRecognitionTask


```swift
public func askPermission() {
    SFSpeechRecognizer.requestAuthorization { (authStatus) in
        NSOperationQueue.main().addOperation {
            switch authStatus {
            case .authorized: // Good to go
                break
            case .denied: // User said no
                break
            case .restricted: // Device isn't permitted
            case .notDetermined: // Don't know yet
                break
            }
        }
    }
}

```

### Code: Recognizing pre-recorded audio
 
// Recognizing pre-recorded audio



### Code: Recognizing live audio

```swift 
// Recognizing live audio

import AVFoundation
import Speech

   

```


[Apple API](https://developer.apple.com/documentation/speech)

Framework prefix : `SF`

[ios-mastery: speech](https://github.com/between40and2/ios-mastery/tree/master/frameworks/media/speech)

