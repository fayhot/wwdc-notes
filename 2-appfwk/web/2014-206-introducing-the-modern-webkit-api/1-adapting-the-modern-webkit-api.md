

## [Adopting the Modern WebKit API](1-adapting-the-modern-webkit-api.md) | Anders Carlsson | 650 | 


### Creating a WKWebView

```objc
WKWebView *webView = [[WKWebView alloc] initWithFrame:myFrame];
```

### Loading a webpage

```objc
NSURL *URL = [NSURL URLWithString:@"http://en.wikipedia.org/wiki"]; 
NSURLRequest *request = [NSURLRequest requestWithURL:URL];
[webView loadRequest:request];
```

### Configurations

```objc
WKWebViewConfiguration *configuration =  [[WKWebViewConfiguration alloc] init];
WKWebView *webView = [[WKWebView alloc] initWithFrame:myFrame configuration:configuration];
```


WKWebView Actions

- goBack:
- goForward:
- reload:
- stopLoading:


WKWebView Properties

Customizing Page Loading




WKNavigationResponse
Name Type
 response
forMainFrame BOOL
canShowMIMEType BOOL



### Decision Handler

- You decide whether to cancel or allow 
- Navigation action
    - WKNavigationActionPolicyCancel
    - WKNavigationActionPolicyAllow
- Navigation response
    - WKNavigationResponsePolicyCancel
    - WKNavigationResponsePolicyAllow
- Asynchronous


## Demo - WKPedia (Mac)| Beth Dakin | 1545- 2700 | p107



### processing title and progress



### remove common wikipedia suffix.



Gestures

Navigation Gestures

```
webView.allowsBackForwardNavigationGestures = YES;
```

Zoom Gestures - OS X

```
webView.allowsMagnification = YES;

```
