
## [Provide Custom Resources](3-provide-custom-resources.md) | | | p54

[`WKURLSchemeHandler`](https://developer.apple.com/documentation/webkit/wkurlschemehandler)



- Allows your app to handle resource loads for a URL scheme
  - Examples  
    - https://www.apple.com 
    - file:///Users/Alex/demo.txt
    - mailto:j.appleseed@icloud.com
- Only custom URL schemes that WebKit doesn’t handle itself
  - let customScheme = "local"
- You should future-proof your custom scheme
  - let customScheme = "apple-local"


### Simple protocol you implement


```swift 
class MyCustomSchemeHandler : NSObject, WKURLSchemeHandler {
    func webView(_ webView: WKWebView, start urlSchemeTask: WKURLSchemeTask) { }
    func webView(_ webView: WKWebView, stop urlSchemeTask: WKURLSchemeTask) { } 
}


### Load something in your view that uses your scheme

```swift
let configuration = WKWebViewConfiguration() configuration.setURLSchemeHandler(MyCustomSchemeHandler(), forURLScheme: “apple-local”)
let webView = WKWebView(frame: getFrame(), configuration: configuration) webView.load(URLRequest(url: URL(string: “apple-local:top“)!))
```


The WKURLSchemeTask sent to your handler represents a resource load
 
```swift
protocol WKURLSchemeTask : NSObjectProtocol { var request: URLRequest
func didReceive(_ response: URLResponse) func didReceive(_ data: Data)
func didFinish()
func didFailWithError(_ error: Error)
}
```


### Deliver the resource data

``` 
func webView(_ webView: WKWebView, start urlSchemeTask: WKURLSchemeTask) { let resourceData = createHTMLResourceData()
let response = ...
urlSchemeTask.didReceive(response) urlSchemeTask.didReceive(resourceData) urlSchemeTask.didFinish()
}
```

### Signal completion

```swift
func webView(_ webView: WKWebView, start urlSchemeTask: WKURLSchemeTask) { 
    let resourceData = createHTMLResourceData()
    let response = ...

    urlSchemeTask.didReceive(response) 
    urlSchemeTask.didReceive(resourceData)
    urlSchemeTask.didFinish()
}
```


## Demo - Providing custom resources | Alex Christensen | | p78


### Providing Custom Resources Demo

- Chose a future-proof URL scheme
- Delivered image data asynchronously

