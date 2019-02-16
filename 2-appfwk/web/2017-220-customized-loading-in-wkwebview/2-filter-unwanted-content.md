## [Filter Unwanted Content](2-filter-unwanted-content.md) | | 1005 | p34

WKContentRuleList

- Same syntax as Content Blocker extensions for Safari
  - Block loads
  - Make content invisible
  - Make insecure loads secure
- WebKit compiles your rules into efficient bytecode


You supply rules in JSON

```json 
[
    {
        "trigger": {
            "url-filter": ".*" 
        },
        "action": {
            "type": "make-https"
        } 
    }
]
```

### Compile your JSON using WKContentRuleListStore

```swift
let jsonString = loadJSONFromBundle()
WKContentRuleListStore.default().compileContentRuleList( forIdentifier: "ContentBlockingRules",
encodedContentRuleList: jsonString) { (contentRuleList, error) in
    if let error = error { return }
    createWebViewWithContentRuleList(ruleList!) 
}
```


WKContentRuleList

### Access previously compiled WKContentRuleList
 
```swift
 WKContentRuleListStore.default().lookUpContentRuleList(forIdentifier: "ContentBlockingRules") { (contentRuleList, error) in
// Use previously compiled content rule list
}
```

### Add compiled WKContentRuleList to your WKWebView’s configuration

```swift
let configuration = WKWebViewConfiguration() 
configuration.userContentController.add(contentRuleList)
```



## Demo -  Managing cookies and filtering content | Alex Christensen | | p50

