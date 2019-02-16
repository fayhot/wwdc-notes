network-statistics.md

## NSURLSession API [Network Statistics](network-statistics.md)| 23:50  | p91

NSURLSessionTaskDelegate new method


[`urlSession(_:task:didFinishCollecting:)`](https://developer.apple.com/documentation/foundation/urlsessiontaskdelegate/1643148-urlsession)

NSURLSessionTaskMetrics

[`URLSessionTaskMetrics`](https://developer.apple.com/documentation/foundation/urlsessiontaskmetrics) |  [`URLSessionTaskDelegate`](https://developer.apple.com/documentation/foundation/urlsessiontaskdelegate) | `urlSession(_:task:didFinishCollecting:)`




NSURLSessionTaskTransactionMetrics

[`URLSessionTaskTransactionMetrics`](https://developer.apple.com/documentation/foundation/urlsessiontasktransactionmetrics)



### Four Categories of Metrics


#### 1 - Request and Response

* request: NSURLRequest
* response: NSURLResponse?

#### 2 - Protocol and Connection

* networkProtocolName: String?
* isProxyConnection: Bool
* isReusedConnection: Bool


#### 3 - Load Info

- resourceFetchType: NSURLSessionTaskMetricsResourceFetchType
  - .networkLoad / .localCache / .serverPush

#### 4 - Connection Establishment and Transmission

Task, DNS, Connection

```swift
fetchStartDate: NSDate?
domainLookupStartDate: NSDate?
domainLookupEndDate: NSDate?
connectStartDate: NSDate?
secureConnectionStartDate: NSDate?
secureConnectionEndDate: NSDate?
connectEndDate: NSDate?
```

HTTP-related

```swift
requestStartDate: NSDate?
requestEndDate: NSDate?
responseStartDate: NSDate?
responseEndDate: NSDate?

```

###

```swift
func urlSession(_ session: URLSession, task: URLSessionTask, didFinishCollecting metrics: URLSessionTaskMetrics) {

    print(metrics)
}





class MySessionDelegate:  NSObject, NSURLSessionTaskDelegate {
    @objc(URLSession:task:didFinishCollectingMetrics:)
    func urlSession(_ session: NSURLSession, task: NSURLSessionTask, didFinishCollecting metrics:
NSURLSessionTaskMetrics) {
      //metrics.redirectCount
      //metrics.taskInterval
      //metrics.transactionMetrics[0].connectStartDate ...
    }
let myDelegate = MySessionDelegate()
let config = NSURLSessionConfiguration.defaultSessionConfiguration()
let myDelegateQueue = NSOperationQueue()
let session = NSURLSession(configuration: config, delegate: myDelegate, delegateQueue: myDelegateQueue)
let url = NSURL(string: "https://www.example.com/")!
let task = session.dataTask(with: url) { (data: NSData?, response: NSURLResponse?, error: NSError?) in
...
}
 
task.resume()
```
