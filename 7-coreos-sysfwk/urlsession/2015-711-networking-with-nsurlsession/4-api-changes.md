## [NSURLSession API changes](4-api-changes.md) | Dan Vinegrad | 3120 | p106

NSURLConnection deprecated in OS X 10.11 and iOS 9.0


### Sharing Cookies -  Between Apps and Extensions

Extensions since last year, iOS 8

- Apps and their extensions have different cookie storages by default
- Can use application groups to get a shared data container
- OS X 10.11 and iOS 9 introduce new API to create a shared cookie storage


NSHTTPCookieStorage


### NSURLSessionStreamTask
TCP/IP networking

- Sometimes need a protocol other than HTTP(S)
- Advantages over NSInputStream / NSOutputStream
  - Asynchronous read/write interface
  - Can automatically get through HTTP proxies
  - New API goodies
- Legacy NSStream support




NSURLSessionStreamTask