3-custom-zone.md


### Atomic Commits - for Custom Zones - Only in Private DB

CloudKit relationship advice

- CloudKit has relationships
- You want consistency
- Public database tradeoffs
- Custom zones give you atomic commits

#### Custom zone features

- Batch operations succeed or fail as a whole
- Failures return CKErrorPartialFailure
  - UserInfo dictionary contains individual errors under CKPartialErrorsByItemID Some records have real failures
  - All others have CKErrorBatchRequestFailed


### Delta Downloads

- Keeping an offline cache
- Some apps need to work while offline Data set is small enough to store locally
- Sync is hard


### Sync Different

Implementing an offline cache

Your app should

- Track local changes
- Send changes to the server
- Resolve conflicts
- Fetch server changes with CKFetchRecordChangesOperation
- Apply server changes
- Save server change token

Zone Subscription

Custom zone features

- Different from query subscriptions
- Push notifications when zone contents update

Custom Zones
Notes on design

- Compartmentalize data
  - Records can’t be moved between zones
  - No cross-zone relationships
- Determines level of updates

