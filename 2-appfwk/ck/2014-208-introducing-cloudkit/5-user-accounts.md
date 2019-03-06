5-user-accounts.md


CloudKit User Accounts

- Identity
- Metadata
- Privacy
- Discovery

### User Identity

- User Record ID
- Stable identifier for this user
- Scoped to the container
- Independent API


```swift
CKContainer.default().fetchUserRecordID { 
    (rid: CKRecord.ID?, error: Error?) in
            
        
}
```


### User Metadata

- User Record
- One per database
- World readable in public database
- Treated like ordinary record
- CKRecordTypeUserRecord
- ... mostly
- Reserved by system Cannot be queried


### User Privacy

- No disclosure by default
- Disclosure requested by application


### User Discovery

Input

- User RecordID Email address Entire address book

Output

- User RecordID
- First and last names

Personally identifying information

Requires opt-in

```swift
CKContainer.default().discoverAllIdentities { 
    (userIdentities : [CKUserIdentity]?, error: Error?) in
            
}
```