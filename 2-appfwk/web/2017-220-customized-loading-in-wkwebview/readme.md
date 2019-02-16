
# [2017 220 Customized Loading in WKWebView](https://developer.apple.com/videos/play/wwdc2017/220/)


Topic|Speaker|Time|Page
---|---|---|---
Manage cookies | | 515 | p15 
[Filter Unwanted Content](2-filter-unwanted-content.md) | | 1005 | p34
[Provide Custom Resources](3-provide-custom-resources.md) | | | p54



## Manage cookies | | 515 | p15


Manage Cookies


WKHTTPCookieStore

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


Add a cookie
NEW
 
let cookie = HTTPCookie(properties: [ HTTPCookiePropertyKey.domain: "canineschool.org", HTTPCookiePropertyKey.path: "/",
HTTPCookiePropertyKey.secure: true,
HTTPCookiePropertyKey.name: "LoginSessionID", HTTPCookiePropertyKey.value: "5bd9d8cabc46041579a311230539b8d1"])
cookieStore.setCookie(cookie!) { webView.load(loggedInURLRequest)
}


Manage Cookies
WKHTTPCookieStore
Retrieve the set of all cookies in a WKWebsiteDataStore
NEW
 
cookieStore.getAllCookies() { (cookies) in for cookie in cookies {
// Find the login cookie
} }





