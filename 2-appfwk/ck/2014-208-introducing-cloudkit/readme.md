# [2014 208 Introducing CloudKit](https://developer.apple.com/videos/play/wwdc2014/208/)


Convenience API
Saving a record Fetching a record Saving modified record




Queries
Predicates

```objc
[NSPredicate predicateWithFormat:@"name = %@", partyName];
[NSPredicate predicateWithFormat:@"%K = %@", dynamicKey, value];
[NSPredicate predicateWithFormat:@"start > %@", [NSDate date]];
CLLocation *location = [[CLLocation alloc] initWithLatitude:37.783 longitude:-122.404];
[NSPredicate predicateWithFormat:@"distanceToLocation:fromLocation:(Location, %@) < 100",
location];
[NSPredicate predicateWithFormat:@"ALL tokenize(%@, 'Cdl') IN allTokens",
                                 @"after session"];
[NSPredicate predicateWithFormat:@"name = %@ AND startDate > %@",
                                 partyName, [NSDate date]];

```


### Performing

```objc

CKQuery *query = ...;
[[publicDatabase performQuery:query
                 inZoneWithID:nil
            completionHandler:^(NSArray *results, NSError *error) {
// astounding error handling when (error != nil)
    if (!error) {
        NSLog(@"Fetch %ld results", (long)[results count]);
        for (CKRecord *record in results) {
            NSLog(@"Found matching party %@", record);
        }
} }];

```

### Big Data, Tiny Phone

- Queries are polls
- Great for slicing through large server data
- Bad for large, mostly static data set
  - Battery life
  - Networking traffic
  - User experience
- What you want is the server running your query
  - ... in the background
  - ... after every record save
  - ... and you want push
