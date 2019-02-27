
# [2016 231 CloudKit Best Practices](https://developer.apple.com/videos/play/wwdc2016/231/)

* Dave Browning, CloudKit Engineer
* Nihar Sharma, CloudKit Engineer

TOC


Topic|Speaker|Time|Page
---|---|---|---
[How Apple uses CloudKit](1-how-apple-uses-cloudkit.md) | Dave Browning
Using the CKOperation API|
Modeling your data|
Handling errors|


## [How Apple uses CloudKit](1-how-apple-uses-cloudkit.md) | Dave Browning 


## Using the CKOperation API

## Modeling your data


## [Handling errors](https://developer.apple.com/videos/play/wwdc2016/231/?time=2269)



Fatal errors
 
public enum CKErrorCode : Int {
   case internalError
   case serverRejectedRequest
   case invalidArguments
   case permissionFailure
}

Operations should not be retried



Retry case
  
public enum CKErrorCode : Int {
   case zoneBusy
   case serviceUnavailable
   case requestRateLimited
}
Implement application-level retry using CKErrorRetryAfterKey



```swift
// Using CKErrorRetryAfterKey
var error = ... // Error from the previous CKOperation
if let retryAfter = error.userInfo[CKErrorRetryAfterKey] as? Double {
    let delayTime = DispatchTime.now() + retryAfter
    DispatchQueue.main.after(when: delayTime) {
        // Initialize CKOperation for a retry
} }
```



Unavailable states
Account unavailable
notAuthenticated
public static let CKAccountChanged: NSNotification.Name
class CKContainer {
    public func accountStatus(completionHandler: (CKAccountStatus, NSError?) -> Void)
}

