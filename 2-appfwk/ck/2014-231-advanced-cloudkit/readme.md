

2014-231-advanced-cloudkit/readme.md

# [2014 231 Advanced CloudKit](https://developer.apple.com/videos/play/wwdc2014/231/)

- Jacob Farkas, Software Engineer


```

CloudKit private database | 650
Modeling your data
Advanced record manipulation | 1550
Handling notifications | | p201
iCloud Dashboard

```


## CloudKit API - Meet NSOperation

### CloudKit Operations - Basic NSOperations

```
@interface NSOperation : NSObject

@end
```

### Basic NSOperationQueue

```
@interface NSOperationQueue : NSObject
- (void)addOperation:(NSOperation *)op;
Starting Operations
- (NSArray *)operations;
- (void)setSuspended:(BOOL)b;
- (BOOL)isSuspended;
    - (void)cancelAllOperations;
@end
```


NSOperation Tips
Dependencies


- Use dependencies between operations
- Dependencies work between queues

### Big Data, Little Phone

- More data than could fit on a single client
- Data downloaded on demand
- No offline use


### Little Data, Lots of Clients

- Data fits on a client
- Every client wants the same data
- Lots of clients
