
# [2015 232 Best Practices for Progress Reporting](https://developer.apple.com/videos/play/wwdc2015/232/)


- Vince Spader Cocoa Frameworks Engineer

Agenda

Topic|Time|Page
---|---|---
Introduction|
[Composition](2-composition.md) | 1155 | p30
Cancellation, pausing, and resuming|  | p90
User interface| 3320 | p96
Best practices| 3440 | p105
The End| | p118


class [`Progress`](https://developer.apple.com/documentation/foundation/progress) since iOS 7

protocol [`ProgressReporting`](https://developer.apple.com/documentation/foundation/progressreporting) since iOS 9

## Introduction

- Makes it easy to report progress in your app across various components
- Cocoa APIs are reporting their progress via NSProgress
  - NSBundleResourceRequest UIDocument NSData
- Helps with localization

```swift
var totalUnitCount: Int64
var completedUnitCount: Int64
var fractionCompleted: Double { get }
```




Units
Bytes
Files
Photos Percentage points Fraction of work Anything


var indeterminate: Bool { get }
Returns true if totalUnitCount < 0 or completedUnitCount < 0



### Demo | 800



## User interface| 3320 | p96


NSProgress properties are key value observable
- Add KVO observers to update your UI
- Not necessarily called on main thread


```swift

progress.addObserver(self, forKeyPath: "fractionCompleted", 
    options: [], context: &observationContext)

override func observeValueForKeyPath(keyPath: ..., object: ..., ..., context: ...) {
    if context == &observationContext && keyPath == "fractionCompleted" {
        NSOperationQueue.mainQueue().addOperationWithBlock {
            let progress = (object as! NSProgress)
            progressView.progress = Float(progress.fractionCompleted)
        }
    }
    else {
         super.observeValueForKeyPath(...)
    } 
}
```

## Best practices| 3440 | p105


Don’t use fractionCompleted to determine completion

- It’s a float
- Use completedUnitCount >= totalUnitCount instead (unless indeterminate or zero)

NSProgress instances cannot be reused

Make a new instance and provide an additional mechanism so clients know

### Performance

- Don’t update completedUnitCount in a tight loop
- Don’t forget that final update to 100%

