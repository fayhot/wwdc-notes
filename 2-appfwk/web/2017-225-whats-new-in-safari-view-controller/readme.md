# [2017 225 What's New in Safari View Controller](https://developer.apple.com/videos/play/wwdc2017/225)




- Chelsea Pugh, Safari Engineer
- Louie Livon-Bemel, Safari Engineer


Use cases

- Browsing the web
- Authenticating with a  third-party service

Agenda

Topic|Speaker|Time|Page
---|---|---|---
• Displaying web content | Chelsea Pugh | 255 | p9
• Matching your app’s style|
Demo - Customizing color | Louie Livon-Bemel | 945 | p46
• iOS 11 improvements|
• Tailoring Safari View Controller| | | | p86
Demo - Tailoring Safari View Controller | Louie Livon-Bemel | 2350 | p107
The End | | 3358 | p121

## Displaying web content | Chelsea Pugh | 255 | p9

SFSafariViewController

- Standard features already implemented
- Present an in-app web browser without the work
- Easily log users in to third-party services

WKWebView

- Manipulate the DOM
- Customize navigations
- Add your own UI


Features from Safari

- AutoFill
- Reader
- 



## Demo - Customizing color | Louie Livon-Bemel | 945 | p46





## iOS 11 improvements | | 1320 | p50


5 

- Drag and Drop
- Status Bar
- Safari View Controller supports window.open()
- Privacy

### Status Bar

Other views can be presented in Safari View Controller
Use UIViewController-based status bar appearance
Set UIViewControllerBasedStatusBarAppearance to YES in Info.plist

### Safari View Controller supports window.open()



### Privacy

Private Browsing




### Customizing Dismiss Button (NEW)

```swift 
enum DismissButtonStyle : Int { 
    case done
    case cancel
    case close 
}
class SFSafariViewController : UIViewController {
    var dismissButtonStyle: SFSafariViewController.DismissButtonStyle
}
```

Choose button depending on your use case Value can be changed while presented



### Customizing the Share Sheet (NEW)

```swift 
protocol SFSafariViewControllerDelegate : NSObjectProtocol {
optional func safariViewController(_ controller: SFSafariViewController,
excludedActivityTypesFor URL: URL, title: String?) -> [UIActivityType] }
```


### Bar Collapsing  (NEW)

```swift 
class Configuration : NSObject, NSCopying { var barCollapsingEnabled: Bool
}
```

- Part of new SFSafariViewController.Configuration
Leave enabled for a more immersive browsing experience Disable if dismiss button should always be shown



## Demo - Tailoring Safari View Controller for your app | Louie Livon-Bemel