

### [Customizing Webpage Content](3-customizing-webpage-content.md) | 2922

- User Scripts
- Script Messages
- Managed by WKUserContentController


### User Scripts [`WKUserScript`](https://developer.apple.com/documentation/webkit/wkuserscript)

- When they run
  - Document start
  - Document end
- Where they run
  - All frames
  - Main frame only


```objc
NSString *myScriptSource = @"alert('Hello, World!')";
WKUserScript *myUserScript = [[WKUserScript alloc] initWithSource:myScriptSource  injectionTime:WKUserScriptInjectionTimeAtDocumentStart , forMainFrameOnly:YES];

[userContentController addUserScript:myUserScript];
```

### What Can User Scripts Do?

- Incredibly powerful
- Modify the document
- Listen for events
- Load resources
- Communicate back to your application



## Demo - WKPedia for iPad | Beth Dakin | 3510 | p167

