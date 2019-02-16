
# [2015 711 Networking with NSURLSession](https://developer.apple.com/videos/play/wwdc2015/711/)


2015-711-networking-with-nsurlsession/readme.md

- Luke Case, Software Engineer
- Andreas Garkuscha, Software Engineer
- Dan Vinegrad, Software Engineer

TOC

Topic|Speaker|Time|Page
---|---|---|---
App Transport Security|Luke Case
[New protocol support in NSURLSession](2-new-protocol-support-in-nsurlsession.md) | Andreas Garkuscha | 1310 | p33
[NSURLSession on watchOS](3-nsurlsession-on-watchos.md) |Dan Vinegrad | 2530 | p100
[NSURLSession API changes](4-api-changes.md) | Dan Vinegrad | 3120 | p106


### NSURLSession

- API for downloading HTTP content
- Rich set of delegate methods
- Background download/upload capability


## App Transport Security|


HTTPS - HTTP over TLS

- Encryption / Integrity / Authentication


```
NSAppTransportSecurity
   NSExceptionDomains
    "example.com"
      NSIncludesSubdomains = YES
      NSExceptionRequiresForwardSecrecy = NO
      NSExceptionMinimumTLSVersion = "TLSv1.1"
```

```
NSAppTransportSecurity
  NSExceptionDomains
    "media.example.com"
      NSExceptionAllowsInsecureHTTPLoads = YES
```


```
NSAppTransportSecurity
  NSAllowsArbitraryLoads = YES
```


```
NSAppTransportSecurity
  NSAllowsArbitraryLoads
  NSExceptionDomains
    "secure.example.com"
    NSExceptionAllowsInsecureHTTPLoads = NO
```


Configuring ATS
Diagnosing issues
Active when you build your app for iOS 9 and OS X El Capitan "http://" to "https://" is automatic
Use NSAllowsArbitraryLoads for quick triage
Log NSURLSession errors
CFNETWORK_DIAGNOSTICS=1



Protecting Customer Data
Next steps
Use HTTPS for new projects
Transition existing apps from HTTP to HTTPS Use exceptions where needed

