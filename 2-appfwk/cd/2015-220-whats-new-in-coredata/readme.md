2015-220-whats-new-in-coredata/readme.md

- Rishi Verma, Core Data Engineer
- Scott Perry, Core Data Engineer


What Is Core Data?
To persist or not to persist Rishi Verma Core Data Engineer


### Object Graph Management

Manage my graph with Core Data

- Bridge your data simply into a Cocoa Model Layer
- Persist data in the back end of your choice

### Automatic Graph Management
Relationships can be complicated...

- Automatic relationship maintenance

### NSFetchRequest
Finding a needle in a haystack

- Find the data you need
- Batching
- Relationship prefetching
- Then tie this with your UI and...

### View and Controller Support

My UI brings all the updates to the users


### Multi-Writer Conflict Handling

On your mark, set that merge policy, and done

CoreData versions all objects

Several types of merge policies available

- Defaults to error
- Persistent store vs. in-memory


### Memory Efficiencies

APIs with benefits

- Excellent memory scalability
- Aggressive lazy loading

### Smaller Footprint Less is more


## Unique Constraints

I got 99 problems and they are all duplicates...


### Find or Create Pattern - Unique constraints

```swift
managedObjectContext.performBlock {
  let createRequest = NSFetchRequest(entityName: "Recipe")
  createRequest.resultType = ManagedObjectIDResultType
  let predicate =
    NSPredicate(format: "source = %@ AND externalID = %@", source,externalID)
  let results = self.managedObjectContext.executeFetchRequest(createRequest)
  if (results.count) {
      //update it!
  } else {
      //create it!
  }
}
```

### One of a Kind - Unique constraints

Unique attributes across all instances of an entity

- Email addresses
- Part numbers
- UPC
- ISBN
- Unique key/value pairs


Best Practices
Unique constraints

- Best for values unmodified after object creation
- Sub-entities may extend constraints
  - Parent (UUID)
  - Sub-entity (UUID, EMAIL)
- Recovery uses merge policies

## Demo - How to utilize unique constraints

## Deleting Multiple Objects - Take one down, pass it around...

Scott Perry Code Generator

## Demo - NSBatchDeleteRequest


## Model Versioning