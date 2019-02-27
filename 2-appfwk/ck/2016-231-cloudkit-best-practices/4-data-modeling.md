
## [Data Modeling](4-data-modeling.md) | | 3035 | p197


- Schema redundancies
- CKReferences
- Parent references

### Schema redundancies

thumbnail1024 



Optimized download

- Fetch only what’s needed
- CKFetchRecordZoneChangesOperation, CKFetchRecordsOperation
- Dynamic UI

### CKReferences

```swift
// Query to find all Photos in an Album
let predicate =  Predicate(format: "AlbumReference == %@", argumentArray: [albumRecord.recordID])
let query = CKQuery(recordType: "Photo",   predicate: predicate)
```

### Parent references

