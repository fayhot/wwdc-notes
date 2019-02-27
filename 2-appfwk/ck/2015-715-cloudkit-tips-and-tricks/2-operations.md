



## [CloudKit Operations](1-operations.md) | | p81

cloud kit operation


query [23]

Queries - In ClownCentral

```swift
let query = CKQuery(recordType: "Photo", 
predicate: NSPredicate(format: "Party == %@", partyRecordID)) 
```

- Parties may have a lot of photos
- Optimize download with CKQueryOperation

limit (say 20 per page)







thumbnail = desiredKeys