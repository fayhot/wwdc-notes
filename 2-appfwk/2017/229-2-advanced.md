
## [Advanced](229-2-advanced.md) 29?

* Open-in-placed
* custom action
* opening transition

### Open-in-placed



3. UIActivityViewController



### Custom Actions

3 diff ways.

[`UIDocumentBrowserAction`](https://developer.apple.com/documentation/uikit/uidocumentbrowseraction)


UIActivityController

### Opening Transition

UIDocumentBrowserTransitionController

```swift

var transitionController: UIDocumentBrowserTransitionController? = nil

func documentBrowser(_ controller: UIDocumentBrowserViewController, didPickDocumentURLs
documentURLs: [URL]) {
  if let documentURL = documentURLs.first {
      let progress = Progress(totalUnitCount: 0)
      transitionController = controller.transitionController(forDocumentURL: documentURL) transitionController?.loadingProgress = progress

      loadDocument(documentURL: documentURL, updateProgress: progress) { present(documentURL: documentURL)
}) }
}
```


### Demo 2 35:00

* open in place
* custom actions
* Zoom transition

#### open in place

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {

    guard url.isFileURL else { return false }
    guard let dbvc = window?.rootViewController as? UIDocumentBrowserViewController else {
        return false
    }

}
```


#### custom actions


#### Zoom transition - 40:00
