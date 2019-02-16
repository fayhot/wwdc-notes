# [2016 711 NSURLSession: New Features and Best Practices](https://developer.apple.com/videos/play/wwdc2016/711/)


One man show

- Jeff Jenkins Software Engineer, Internet Technologies (Speaker)
- Andreas Garkuscha Software Engineer, Internet Technologies (Demo)


Topic|Time|Page
---|---|---
1 Evolving NSURL|
1.1 Review |
1.2 HTTP/2 | 1130
1.3 NSURLSession API - Network statistics | | p91
2 Session API Security|
Security - Never an afterthought| 3620 | p159
3 Best practices and tips|
The End|4203



NSURLSession Example

Benefits

- HTTP/1.1, SPDY, HTTP/2
- App Transport Security (ATS)
- HTTP Strict Transport Security (HSTS) Cache, cookies, proxy, authentication Configuration


NSURLSession Example | 900


```swift
let config = NSURLSessionConfiguration.defaultSessionConfiguration()
let session = NSURLSession(configuration: config)

let url = NSURL(string: "https://www.example.com/")!
let task = session.dataTask(with: url) { (data: NSData?, response: NSURLResponse?, error:
NSError?) in
... }
task.resume()

```


### Review

Summary: Three-step process

- Configuration
- Session
- Tasks



one-session-many-tasks


## [HTTP/2](1_2-http-2.md) | 1130



HTTP/2 Protocol

* Multiplexing and concurrency
* Header compression
* Stream priorities
* Server Push (NEW)

### Demo - HTTP/2 Server Push (Andreas Garkuscha) | 1810 | p81





## Security - Never an afterthought| 3620 | p159


```
$ nscurl https://insecure.example.com/

nscurl[1234:123456] NSURLSession/NSURLConnection HTTP load failed
(kCFStreamErrorDomainSSL, -9824)

$ nscurl —-enable-rc4 https://insecure.example.com/

Enabling RC4 cipher suites
<html><body><h1>It works!</h1></body></html>

```

### App Transport Security

NSAllowsArbitraryLoadsInWebContent
NSRequiresCertificateTransparency
