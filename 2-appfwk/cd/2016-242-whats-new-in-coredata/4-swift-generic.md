
## [Generics](4-swift-generic.md) | | 2535 | 

### Generics - Better living through types

New protocol `NSFetchRequestResult`

- `NSManagedObject` (and subclasses)
- `NSManagedObjectID` 
- `NSDictionary`
- `NSNumber`

```swift
NSFetchRequest<ResultType>
NSManagedObjectContext.fetch(NSFetchRequest<ResultType>) throws -> [ResultType]
NSFetchedResultsController<ResultType>
```


### NSFetchedResultsController ❤ UICollectionViewDataSourcePrefetching

```swift
func collectionView(_ collectionView: UICollectionView,
                    prefetchItemsAt indexPaths: [IndexPath]) {
    let fetchRequest: NSFetchRequest<Event> = Event.fetchRequest()
    fetchRequest.returnObjectsAsFaults = false
    let objects = indexPaths.map({ (index) -> Event in
        self.fetchedResultsController.object(at: index)
    })
    fetchRequest.predicate = Predicate(format: "SELF IN %@", objects as CVarArg)
    let asyncFetchRequest = NSAsynchronousFetchRequest(fetchRequest: fetchRequest,
        completionBlock: nil)
    do {
        try fetchedResultsController.managedObjectContext.execute(asyncFetchRequest)
    } catch {} 
}
```

> 2016 What’s New in UICollectionView

### Now Available 

NSFetchedResultsController on macOS

### Common Operations

Operation|Type casts and strings|Subclasses gain superpowers
---|---|---
Get an entity description|`NSEntityDescription.entity(forEntityName: "Entity", in: managedObjectContext)`|`Subclass.entity()`
Create a fetch request|`NSFetchRequest(entityName: "Entity") as! NSFetchRequest<Subclass>`|Subclass.fetchRequest()
Create a managed object|`NSEntityDescription.insertNewObjectForEntityForName("Entity", inManagedObjectContext:managedObjectContext) as! Subclass`|`Subclass(context: managedObjectContext)`
Execute a fetch request| |try context.fetch(fetchRequest)



