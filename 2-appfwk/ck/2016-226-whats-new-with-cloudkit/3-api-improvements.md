
## [API Improvements](3-api-improvements.md)

* Long Lived Operations
* CKOperation Timeouts
* Handling Many Record Zones
* Fetching Multiple Change Sets


### Long Lived Operations

Don’t repeat your work


### CKOperation Timeouts

#### How long do you want to wait?

QoS | Behavior on broken network
--|--
userInteractive | timeout after 60 seconds
userInitiated | timeout after 60 seconds
utility | timeout after 7 days
background | timeout after 7 days
default | timeout after 7 days

* Network inactivity
  * Use the timeoutIntervalForRequest property on CKOperation
  * Default value is 60 seconds
* Start-to-finish timeout
  * Use the timeoutIntervalForResource property on CKOperation
  * Default value is 7 days
  * CKOperation may stay around longer

### Handling Many Record Zones

Reduce payloads and roundtrips

New | Deprecated
-- | --
CKDatabaseSubscription |
CKFetchDatabaseChangesOperation | CKFetchRecordZonesOperation
CKFetchRecordZoneChangesOperation | CKFetchRecordChangesOperation


### Fetching Multiple Change Sets

```swift
public class CKFetchRecordZoneChangesOperation : CKDatabaseOperation {
   public var recordZoneChangeTokensUpdatedBlock: ((CKRecordZoneID, CKServerChangeToken?,
      Data?) -> Void)?
}
```