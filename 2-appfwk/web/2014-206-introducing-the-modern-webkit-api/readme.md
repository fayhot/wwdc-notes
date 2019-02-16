## [2014 206 Introducing the Modern WebKit API](https://developer.apple.com/videos/play/wwdc2014/206)


The modern WebKit framework enables developers to integrate web content into their native app experience with more features and fewer lines of code. Dive into the latest WebKit enhancements including modern Objective-C features such as blocks and explicit object types, advanced bridging between JavaScript and Objective-C, increased JavaScript performance via WebKit's super-fast JIT, and more—all delivered in an API unified for both iOS and OS X.



- Embedding web content in your app
- Taking advantage of new features of the WebKit API
- Customizing how your app interacts with web content



2014-206-introducing-the-modern-webkit-api/readme.md


## The Modern WebKit API



- Same on iOS and OS X
- Modern
- Streamlined
- Multi-process architecture



Features

- Responsive scrolling
- Fast JavaScript
- Built-in gestures
- Easy app-webpage communication


Multi-process Architecture 

Web content runs in its own process
Consistently responsive
Energy efficient



## Adopting the Modern WebKit API | 650 | 


### Creating a WKWebView

WKWebView *webView = [[WKWebView alloc] initWithFrame:myFrame];


###Loading a webpage

NSURL *URL = [NSURL URLWithString:@"http://en.wikipedia.org/wiki"]; NSURLRequest *request = [NSURLRequest requestWithURL:URL]; 
[webView loadRequest:request];


### Configurations

WKWebViewConfiguration *configuration =  [[WKWebViewConfiguration alloc] init];
WKWebView *webView = [[WKWebView alloc] initWithFrame:myFrame  configuration:configuration];



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


## Demo - WKPedia | Beth Dakin | 1545 | p107


End of Demo | 2700

Gestures
Navigation Gestures
webView.allowsBackForwardNavigationGestures = YES;


Zoom Gestures
OS X
webView.allowsMagnification = YES;


