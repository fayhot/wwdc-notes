2-api-fundamental.md


### Containers

- CKContainer
- One container per app Data segregation
- User encapsulation
- Managed by the developer
  - Managed via WWDR portal
  - Unique across all developers
- Can be shared between apps


### Databases

- CKDatabase
- Every app has access to two databases
  - Public Database
  - Private Database

```  
CKDatabase *publicDatabase = [[CKContainer defaultContainer] publicCloudDatabase]; !
CKDatabase *privateDatabase = [[CKContainer defaultContainer] privateCloudDatabase];
```


X|Public Database|Private Database
---|---|---
Data Type|Shared Data|Current User’s Data
Account|Required for Writing | Required
Quota|Developer|User
Default Permissions|World Readable|User Readable
Editing Permissions|iCloud Dashboard Roles|N/A






## Records

- CKRecord
- Structured Data
- Wraps key/value pairs
- Record Type
- Just-in-time schema
- Metadata


Record Values

- NSString
- NSNumber
- NSData
- NSDate
- CLLocation
- CKReference
- CKAsset
- Arrays of the above


```objc

CKRecord *party = [[CKRecord alloc] initWithRecordType:@“Party”];
// setting values
[party setObject:@"Post Presentation Beers"
          forKey:@"summary"];
NSDate *startDate = [NSDate dateWithTimeIntervalSinceNow:30.0 * 60.0];
party[@"start"] = startDate;
// accessing values
NSString *summary = [party objectForKey:@"summary"];
NSDate *startDate = party[@"start"];
```

### Record Zones

### Record Identifiers

```objc
@interface CKRecordID : NSObject <NSSecureCoding, NSCopying> ...
@property (nonatomic, readonly, strong) NSString *recordName; @property (nonatomic, readonly, strong) CKRecordZoneID *zoneID; !
@end
```

- Created by the client
- Fully normalized: they represent the location of the record
- External data set foreign key

### References

- CKReference
- Server Understands Relationship
- Cascade Deletes
- Dangling Pointers
- Back References

```objc

CKRecord *clown = [[CKRecord alloc] initWithRecordType:@"Clown"];
CKRecord *party = [[CKRecord alloc] initWithRecordType:@"Party"]; CKReference *partyReference = [[CKReference alloc]
                                 initWithRecord:party
                                 action:CKReferenceActionNone];
clown[@"party"] = partyReference;
CKRecordID *wellKnownID = [[CKRecordID alloc] initWithRecordName:@"WellKnownParty"];
CKReference *wellKnownReference = [[CKReference alloc] initWithRecordID:wellKnownID
                                 action:CKReferenceActionNone];
clown[@"party"] = wellKnownReference;
```


### Assets

- CKAsset
- Large, unstructured data
- Files on disk
- Owned by CKRecords
- Garbage collected
- Efficient uploads and downloads