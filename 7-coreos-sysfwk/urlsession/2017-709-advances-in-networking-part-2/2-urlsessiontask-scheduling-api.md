


## [URLSessionTask Scheduling API](2-urlsessiontask-scheduling-api.md) | Jeff Jenkins| 900 | 

### Introduction

Background URLSession

- Uploads and downloads continue while your app is not running
- System monitors conditions (for example, network, battery, etc.) for you
- App launched
  - When delegate response is required
  - When tasks are complete

[`UIApplicationDelegate`](https://developer.apple.com/documentation/uikit/uiapplicationdelegate)

[`application(_:performFetchWithCompletionHandler:)`](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1623125-application)

[`application(_:handleEventsForBackgroundURLSession:completionHandler:)`](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622941-application)

App State = Running, Suspended, Background


### Background App Refresh

What is it?

- Need data from network to present fresh information to user
  - Stock prices, flight status News, social network feed Weather forecast
- Applies to apps and watchOS complications

See [2013 What’s New with Multitasking] , [2016 Keeping Your Watch App Up to Date]

### Room for Improvement

- Extra background launch just to create a URLSessionTask to fetch future data
- Extra launch impacts battery life
  - Context may change between request creation and start of networking
- Stale request wastes network data
  - System lacks information about your task to know the best time to schedule it


### URLSessionTask Scheduling API

- Indicate the desired start time of a URLSessionTask
- New URLSessionTask property var earliestBeginDate: Date?
  - Guaranteed that task will not begin networking earlier than this
  - Only applicable to background URLSession

### Background App Refresh in Action

Original workflow

Improved workflow


### URLSessionTask Scheduling API (NEW)

- Opportunity to alter future request when system is ready to begin networking
- New URLSessionTaskDelegate method `urlSession(_:task:willBeginDelayedRequest:completionHandler:)`
  - Only called for tasks with earliestBeginDate set
  - Background URLSession only
  - Optional—not required to take advantage of URLSessionTask scheduling
  - Completion handler—proceed, change request (URL and headers), or cancel


### Background App Refresh in Action

Advanced workflow

### URLSessionTask Scheduling API

- Indicate estimated transfer size of each URLSessionTask
- Allows better background task scheduling by the system
- Two new URLSessionTask properties:
  - var countOfBytesClientExpectsToSend: Int64 var countOfBytesClientExpectsToReceive: Int64
- Provide “best guess” (approximate upper bound)
  - or NSURLSessionTransferSizeUnknown

```swift
// URLSessionTask Scheduling API
// Example 1: Scheduling a background task to start no earlier than 2 hours in the future
let config = URLSessionConfiguration.background(withIdentifier: "...")
let session = URLSession(configuration: config  , delegate: ..., delegateQueue: ...)



var request = URLRequest(url:  URL(string:"https://www.example.com/" )!)
request.addValue("...", forHTTPHeaderField: "...")

let task = session.downloadTask(with: request)

 
// Indicate desired scheduling
task.earliestBeginDate =  Date (timeIntervalSinceNow: 2 * 60 * 60)

// Request is small (no body, one added header) and response is ~2 KiB
task.countOfBytesClientExpectsToSend
task.countOfBytesClientExpectsToReceive

task.resume()
```

```swift
// URLSessionTask Scheduling API
// Example 2: Altering HTTP request headers to avoid a stale request
 
func urlSession(_ session: , task:   , willBeginDelayedRequest request:
, completionHandler: (   .   , URLRequest?) -> ){
    var updatedRequest = request
    updatedRequest.addValue("...", forHTTPHeaderField: "...")
    completionHandler(.useNewRequest, updatedRequest) 
}
```


### Recap

- Background URLSession allows apps to upload and download when not running
- New URLSessionTask scheduling API gives you control
  - Delay tasks to when you need them for the freshest information
  - Opportunity to alter tasks before network load begins to avoid stale requests
- Help us deliver the best customer experience
  - Specify expected byte counts for every URLSessionTask

