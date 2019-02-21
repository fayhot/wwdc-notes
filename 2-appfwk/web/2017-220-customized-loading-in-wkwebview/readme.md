
# [2017 220 Customized Loading in WKWebView](https://developer.apple.com/videos/play/wwdc2017/220/)


- Brady Eidson, Safari and WebKit Engineer
- Alex Christensen, Safari and WebKit Engineer


Topic|Speaker|Time|Page
---|---|---|---
Manage cookies | Brady Eidson | 515 | p15 
[Filter Unwanted Content](2-filter-unwanted-content.md) |Brady Eidson | 1005 | p34
Demo -  Managing cookies and filtering content | Alex Christensen | 1610 | p50
[Provide Custom Resources](3-provide-custom-resources.md) | Brady Eidson | 2245 | p54
Demo - Providing custom resources | Alex Christensen | | p78
The End ||3635|


## Manage cookies | Brady Eidson | 515 | p15


### [`WKHTTPCookieStore`](https://developer.apple.com/documentation/webkit/wkhttpcookiestore)

- Add and remove individual cookies
- Access all cookies visible to a WKWebView
- Including HTTP-only cookies
- Observe the cookie store for changes



Get to a WKWebViews cookie store through its websiteDataStore

```swift
open class WKWebsiteDataStore : NSObject, NSCoding { 
    open var httpCookieStore: WKHTTPCookieStore { get }
}
let cookieStore = webView.configuration.websiteDataStore.httpCookieStore;

```


### Add a cookie (NEW)

```swift
let cookie = HTTPCookie(properties: [   
    HTTPCookiePropertyKey.domain: "canineschool.org", 
    HTTPCookiePropertyKey.path: "/",
    HTTPCookiePropertyKey.secure: true,
    HTTPCookiePropertyKey.name: "LoginSessionID", 
    HTTPCookiePropertyKey.value: "5bd9d8cabc46041579a311230539b8d1"])

cookieStore.setCookie(cookie!) { 
    webView.load   (loggedInURLRequest)
}
```

### Manage Cookies - WKHTTPCookieStore (NEW)

Retrieve the set of all cookies in a WKWebsiteDataStore

```swift
cookieStore.getAllCookies() { (cookies) in 
    for cookie in cookies {
        // Find the login cookie
    } 
}
```
