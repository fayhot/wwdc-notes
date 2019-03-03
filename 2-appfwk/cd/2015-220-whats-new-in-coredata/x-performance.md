## Core Data Performance


Apps Improve

- Models get more complex
- Stores get larger
- Queries get more interesting
- Apps stay fast!



Slow Can Be Surprising

- Scale differs between development and production
- The simulator is faster than the device
- Users use devices in production


## Find Problems Before They Find You - Predicting the future with tools


### Relationship Faults - Prefetch the objects you’re going to use

```swift
var recipeRequest = NSFetchRequest(entityName:"Recipe")
let sortDescriptor = NSSortDescriptor(key:"name", ascending: true)
recipeRequest.sortDescriptors = [sortDestcriptor]
recipeRequest.relationshipKeyPathsForPrefetching = ["type"]
context.executeFetchRequest(recipeRequest)
```


```swift

var ingredientRequest = NSFetchRequest(entityName:"Ingredient")
ingredientRequest.predicate = NSPredicate(format:"recipe = %@",
    argumentArray:[recipe])
context.executeFetchRequest(ingredientRequest)
```


### Large Fetches - Take advantage of batching

```swift
var recipeRequest = NSFetchRequest(entityName:"Recipe")
let sortDescriptor = NSSortDescriptor(key:"name", ascending: true)
recipeRequest.sortDescriptors = [sortDestcriptor]
recipeRequest.fetchBatchSize = 30
context.executeFetchRequest(recipeRequest)
```




### Complex Fetches - Verify a better plan

```
sqlite> EXPLAIN QUERY PLAN SELECT 0, t0.Z_PK, t0.Z_OPT, t0.ZEXTERNALID,
t0.ZINSTRUCTIONS, t0.ZNAME, t0.ZOVERVIEW, t0.ZPREPTIME, t0.ZSOURCE,
t0.ZTHUMBNAILIMAGE, t0.ZIMAGE, t0.ZTYPE FROM ZRECIPE t0 WHERE  NOT ( t0.Z_PK
IN (SELECT n1_t0.Z_PK FROM ZRECIPE n1_t0 GROUP BY n1_t0.ZSOURCE,
n1_t0.ZEXTERNALID ));
sele  order          from  deta
----  -------------  ----  ----
0 0 0 0 1 0
0     SCAN TABLE ZRECIPE AS t0
0     EXECUTE LIST SUBQUERY 1
0     SCAN TABLE ZRECIPE AS n1_t0 USING COVERING INDEX
      ZRECIPE_ZSOURCE_ZEXTERNALID
```

### Complex Fetches - Irreducible complexity

Get off the main thread

- Private queue context
- NSAsynchronousFetchRequest


## Look for Problem Patterns

- Relationship faults
  - Lots of small queries slow down your app
- Large fetches
  - Make Core Data do the work
- Complex fetches
  - Add indices and try more powerful predicates
  - Avoid blocking UI threads
