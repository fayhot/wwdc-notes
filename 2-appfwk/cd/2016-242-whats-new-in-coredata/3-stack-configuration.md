


[Setting Up Core Data](3-stack-configuration.md)| Scott Perry Chordate | 2020 |p84

// Add a Persistent Store
 
  
persistentStoreCoordinator.addPersistentStore(ofType: type, configurationName: configuration,
at: url, options: options)

[`NSPersistentStoreDescription`](https://developer.apple.com/documentation/coredata/nspersistentstoredescription) (New in iOS 10)


Easy customization of common options 

- Read-only
- Timeout
- Automatic lightweight migration
- Automatic mapping model inference
- Add store asynchronously



```swift
storeDescription.shouldAddStoreAsynchronously = true
persistentStoreCoordinator.addPersistentStore(
    with: storeDescription,
    completionHandler: { (storeDescription, error) in
    
    if let error = error { 

    }else {

    } 
})
```


### Representing a Core Data Stack

[`NSPersistentContainer`](https://developer.apple.com/documentation/coredata/nspersistentcontainer)


- Encapsulates model configuration
- Name
- Store descriptions
- Loads stores

### In the Past

```swift
 lazy var applicationDocumentsDirectory: NSURL = {
    let urls = NSFileManager.defaultManager().urlsForDirectory(.documentDirectory,
        inDomains: .userDomainMask)
    return urls[urls.count-1]
}()

lazy var managedObjectModel: NSManagedObjectModel = {
    let modelURL = NSBundle.main().urlForResource("AppName", withExtension: "momd")!
    return NSManagedObjectModel(contentsOf: modelURL)!
}()


lazy var persistentStoreCoordinator: NSPersistentStoreCoordinator = {
    
}()


lazy var managedObjectContext: NSManagedObjectContext = {
    let coordinator = self.persistentStoreCoordinator
    var managedObjectContext = NSManagedObjectContext(concurrencyType: .mainQueueConcurrencyType)
    managedObjectContext.persistentStoreCoordinator = coordinator
    return managedObjectContext
}()
```

### Now

```swift
 
lazy var persistentContainer: NSPersistentContainer = {
    let container = NSPersistentContainer(name: "AppName")
    container.loadPersistentStores(completionHandler: { (storeDescription, error) in
        if let error = error {
            // Replace this implementation with code to handle the error appropriately.
            fatalError("Unresolved error \(error), \(error.userInfo)")
        } 
    })
    return container
}()
```

### Where Did It All Go?
Default values and behavior

- Model looked up by container name
- Store filename determined by container name
- Store directory provided by the container class

### NSPersistentContainer

Support for common workflows

- Main queue context property
- Private queue context factory method
- Method for enqueuing background work

```swift
// Doing Background Work With a Container

let context = NSManagedObjectContext(concurrencyType: .privateQueueConcurrencyType)
context.persistentStoreCoordinator = persistentStoreCoordinator
context.perform({

})

 
container.performBackgroundTask({ (context) in
    // ...
})
```

### NSManagedObjectContext - Speaking of common workflows...

- New property `automaticallyMergesChangesFromParent`
- Works with generation tokens

