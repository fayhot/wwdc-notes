

### [Customizing Webpage Content](3-customizing-webpage-content.md) | 2922

- User Scripts
- Script Messages
- Managed by [`WKUserContentController`](https://developer.apple.com/documentation/webkit/wkusercontentcontroller)


### User Scripts [`WKUserScript`](https://developer.apple.com/documentation/webkit/wkuserscript)

- When they run
  - Document start
  - Document end
- Where they run
  - All frames
  - Main frame only


```objc
NSString *myScriptSource = @"alert('Hello, World!')";
WKUserScript *myUserScript = [[WKUserScript alloc]  
    initWithSource:myScriptSource  
    injectionTime:WKUserScriptInjectionTimeAtDocumentStart , 
    forMainFrameOnly:YES];

[userContentController addUserScript:myUserScript];

```

### What Can User Scripts Do?

- Incredibly powerful
  - Modify the document
  - Listen for events
  - Load resources
  - Communicate back to your application

### Script Messages

- Sent as JSON
- Converted to Objective-C types


### Registering a Script Message Handler

WKScriptMessageHandler protocol 

```objc
- (void)userContentController:(WKUserContentController
*)userContentController didReceiveScriptMessage:(WKScriptMessage *)message;

[userContentController addScriptMessageHandler:handler name:@"myName"];

```

### 2. Posting messages

```js
window.webkit.messageHandlers.<name>.postMessage();
function postMyMessage() {
    var message = { 'message' : 'Hello, World!', 'numbers' : [ 1, 2, 3 ] };
    window.webkit.messageHandlers.myName.postMessage(message);
}
```

### 3. Receiving messages

```objc
- (void)userContentController:(WKUserContentController
*)userContentController didReceiveScriptMessage:(WKScriptMessage *)message
{
    NSLog(@"Message: %@", message.body);
}
```



### The webpage can call postMessage

- Great for allowing webpages to interact with your app
- Handle invalid messages


