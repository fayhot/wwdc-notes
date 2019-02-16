## [URLSession Adaptable Connectivity API](1-urlsession-adaptable-connectivity-api.md) | Jeffrey Twu | | p3



- URLSession with defaultSessionConfiguration fetches or fails
- Lack of connectivity causes URLSessionTasks to immediately fail with errors
  - NSURLErrorNotConnectedToInternet
  - NSURLErrorCannotConnectToHost
- Background URLSession has built-in support for monitoring connectivity

### Unsatisfactory Connectivity - Examples

- No Ethernet cable, not connected to Wi-Fi network, no cellular signal
- Device in Airplane Mode
- Only cellular connectivity, but allowsCellularAccess prohibits cellular
- VPN not connected


### Current Solutions

- Each app must manually retry URLSessionTasks once connectivity is satisfactory
- When is that?
  - Monitor conditions with SCNetworkReachability API
  - Polling/manual retry
- Current mechanisms cannot guarantee connection establishment will succeed



Wouldn’t it be easier to say...

“Please fetch me this resource when the network is available.”


### URLSession Adaptable Connectivity API - Built-in connectivity monitoring (NEW)

- Indicates URLSession should monitor network conditions and wait to start tasks
- Begins network load once connectivity is satisfactory instead of delivering errors
  - No longer a need to monitor connectivity and manually retry requests
- New URLSessionConfiguration property var waitsForConnectivity: Bool
  - Not necessary for background URLSession (does this automatically)



### Insufficient connectivity notification (NEW)

- Notification that a URLSessionTask is waiting for connectivity before starting
- Opportunity to alter app behavior or indicate status
- New URLSessionTaskDelegate method 
  - `urlSession(_:taskIsWaitingForConnectivity:)`
- Optional—not required to take advantage of adaptable connectivity functionality
- Called at most one time for each URLSessionTask

### When to enable it

- No downside—if connectivity is available, tasks will start right away
- General recommendation
  - Always enable waitsForConnectivity
- Exception
  - Requests that must be completed immediately, or not at all  for example, “Fill or Kill” stock trading transaction


### What to expect

- Create and resume URLSessionTask
- If insufficient connectivity urlSession(_:taskIsWaitingForConnectivity:) called (if implemented)
- URLSession waits until connectivity is satisfactory
- Existing URLSessionDelegate methods/completion handler called, just as before


```swift
 // URLSession Adaptable Connectivity API
 // Example 1: Enabling adaptive connectivity
 
let config =  URLSessionConfiguration.default 
config.waitsForConnectivity =  true

let session = URLSession(configuration: config)
let url = URL(string: "https://www.example.com/")!

let task = session.dataTask(with: url) { 
    (data: Data?, response: URLResponse?, error: Error?) in

}
task.resume()
```

### Maintain Robustness to Failures

- Adaptable connectivity applies to establishing new connections
- Network and server problems can still occur once connected, causing failures
  - NSURLErrorConnectionLost
  - NSURLErrorTimedOut
- Application-specific logic must determine resolution
  - Refer to Technical Q&A QA1941 on Apple Developer website  Handling “The network connection was lost” Errors

### Recap

- Polling for network connectivity is prone to problems
- Avoid retrying URLSessionTasks due to lack of network connectivity
- Let URLSession do the work
  - Monitors network conditions for you
  - Begins loading your URLSessionTask once connectivity is satisfactory

