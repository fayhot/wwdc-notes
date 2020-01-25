
## [Demo - WKPedia for iPad](4-demo-wkpedia-ipad.md) | Beth Dakin | 3510 | p167

### Hide sidebar and TOC

```js
var styleELement = document.createElement('style');
document.documentElement.appendChild(styleELement);
styleELement.textContent = '.toc { display : none !important;} #mw-panel {display: none !important!} #content {margin : 0px 10px 0px 10px !important;};';
```



### TOC into native TableView | 4000


```js 

var entries = [];

var tocLinks = document.querySelectorAll('.toc li.tocLevel-1 a');

for (var i=0; i < tocLinks.length; ++i) {
    var tocLink = tocLinks[i];

    var tocText = tocLink.querySelector('.toctext');
    if (!tocText) break;

    var entry = {'title': tocText.textContent, 'urlString': tocLink.href};
    entries.push(entry);
}

webkit.messageHandlers.didFetchTableOfContents.postMessage(entries);
```

### Debugging in Safari (Develop menu) | 4310


