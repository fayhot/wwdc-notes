



### Little Data, Many Clients

Personal notes for parties

- Private database
- Offline use
- Small amount of data needed on all devices


### Private Database Downloads

```swift
let notesZone = CKRecordZone(zoneName: "NotesZone")
```

Two main ways:

- CKQueryOperation
- Delta downloads using CKFetchRecordChangesOperation 
  - Custom zone with CKRecordZoneCapabilityFetchChanges


### Storing Data Locally [30?] 

How do we fetch changes from our custom zone in order to keep that cache up to date? [34:10]

When do we use ChangeOperation..  - Anser : Subscription .

Archiving system fields

```swift
let record = ...
let archivedData = NSMutableData()
let archiver = NSKeyedArchiver(forWritingWithMutableData: archivedData)
archiver.requiresSecureCoding = true
record.encodeSystemFieldsWithCoder(archiver)
archiver.finishEncoding()
```

### Unarchiving system fields

```swift

let record = ...
let archivedData = NSMutableData()
let archiver = NSKeyedArchiver(forWritingWithMutableData: archivedData)
archiver.requiresSecureCoding = true
record.encodeSystemFieldsWithCoder(archiver)
archiver.finishEncoding()
```

### Efficiently Fetching Changes

- CKFetchRecordChangesOperation
- Notifications using CKSubscription
  - Silent notifications