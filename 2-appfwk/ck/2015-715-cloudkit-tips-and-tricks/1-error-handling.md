
## [error handling](1-error-handling.md)

### account

```swift
extension NSNotification.Name {
    static let CKAccountChanged: NSNotification.Name
}
```


### retry

Retrying Operations 

Poor network conditions
-   CKErrorNetworkFailure

Busy servers

-   CKErrorServiceUnavailable
-  CKErrorZoneBusy

### Rate Limiting

- CKErrorRequestRateLimited
- Mitigates application bugs
- Client-side throttle
- CKErrorRetryAfterKey


### Handling Conflicts | | p59

