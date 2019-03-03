
## [API Enhancements](2-api-enhancements.md)

### hasPersistentChangedValues - NSManagedObject

- var hasPersistentChangedValues: Bool { get }
- No false positives setting a value to itself
- Skips transient properties


### objectIDsForRelationshipNamed - NSManagedObject

- `func objectIDsForRelationshipNamed(key: String) -> [NSManagedObjectID]`
- Reads cache or fetches the objectIDs
- Doesn’t materialize entire relationship
- Useful working with large, many-to-many relationships


```swift
let relations = person.objectIDsForRelationshipNamed("family")
let fetchFamily = NSFetchRequest(entityName: "Person")
fetchFamily.fetchBatchSize = 100
fetchFamily.predicate = NSPredicate(format: "self IN %@", relations)
let batchedRelations = managedObjectContext.executeFetchRequest(fetchFamily)
for relative in batchedRelations {
    // work with relations 100 rows at a time
}
```

### refreshAllObjects - NSManagedObjectContext

- `func refreshAllObjects()`
- Affects all registered objects in a context
- Preserves unsaved changes
- Managed Object references remain valid
- Useful for breaking retain cycles


### mergeChangesFromRemoteContextSave - NSManagedObjectContext

```swift
class func mergeChangesFromRemoteContextSave(
    changeNotificationData: [NSObject : AnyObject], 
    intoContexts contexts: [NSManagedObjectContext])
```

- Better for changes from different coordinators
- Fetches latest row data
- Handles ordering with nested contexts

### No Love for Exceptions - This is not the data you are looking for

- Why is Core Data unable to fulfill a fault?
- Managed objects are implicit futures
  - Cocoa place holders for a row of data
  - Often lazily loaded
  - Part of a larger graph
- Data deleted out from underneath this reference

### shouldDeleteInaccessibleFaults - NSManagedObjectContext

- `var shouldDeleteInaccessibleFaults: Bool`
- Defaults to YES
- Does not effect APIs with error parameters
- Bad faults marked deleted
- Missing data treated as NULL/nil/0

### NSPersistentStoreCoordinator API - It’s my file and I’ll do what I want to

- Truncating and copying databases
- Don’t bypass the API layers
  - NSFileManager and POSIX are bad for databases
  - Will corrupt your files if open connections exist
- Deleting a file with open locks ends badly...very badly


### destroyPersistentStoreAtURL - NSPersistentStoreCoordinator

```swift
func destroyPersistentStoreAtURL(
    url: NSURL, 
    withType storeType: String,
    options: [NSObject : AnyObject]?) throws
```

- Honors locking protocols
- Handles details reconfiguring emptied files
  - Journal mode, page size, etc.
  - Need to pass same options as addToPersistentStore
  - Accidentally switching journal modes can deadlock



### replacePersistentStoreAtURL - NSPersistentStoreCoordinator

```swift
func replacePersistentStoreAtURL(
    destinationURL: NSURL, 
    destinationOptions: [NSObject : AnyObject]?, 
    withPersistentStoreFromURL sourceURL: NSURL,
    sourceOptions: [NSObject : AnyObject]?, 
    storeType: String) throws
```

- Same pattern as destroyPersistentStoreAtURL
- If destination doesn’t exist, this does a copy

