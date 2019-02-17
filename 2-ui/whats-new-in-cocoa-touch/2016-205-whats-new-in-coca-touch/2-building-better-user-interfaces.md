

## [Building better user interfaces](2-building-better-user-interfaces.md) | | p99

Accessibility Inspector


Speech Recognition

SFSpeechRecognizer

Continuous speech recognition
From audio files or audio buffers
Optimized for free-form dictation or search-style strings
let recognizer = SFSpeechRecognizer()
let request = SFSpeechURLRecognitionRequest(url: audioFileURL)
recognizer?.recognitionTask(with: request, resultHandler: { (result, error) in
   print(result?.bestTranscription.formattedString)
})


 Smarter Text Input
Semantic tagging of text fields, text views and web content
Provides intelligent suggestions


Dynamic Type
Content size category trait
No longer a property on UIApplication No need to listen to notifications
Now available in extensions

label.font = UIFont.preferredFont(forTextStyle: UIFontTextStyleBody)
label.adjustsFontForContentSizeCategory = true

Improved Customization
Tab bar items
Custom badge colors and text attributes Customizable unselected Tint Color
tabBarItem.badgeColor = UIColor.white()
badgeTextAttributes = [ NSForegroundColorAttributeName : UIColor.blue(), 
NSFontAttributeName : UIFont.italicSystemFont(ofSize: 12) ] tabBarItem.setBadgeTextAttributes(textAttributes: badgeTextAttributes, 
                                    forState: UIControlStateNormal)
tabBar.unselectedTintColor = UIColor.brown()



Peek & Pop
Improved WKWebView Support
Fine control of Peek & Pop behaviors Custom view controllers
Preview actions
Pop inside your app
public func webView(_ webView: WKWebView,  
shouldPreviewElement elementInfo: WKPreviewElementInfo) -> Bool
public func webView(_ webView: WKWebView,  
previewingViewControllerForElement elementInfo: WKPreviewElementInfo, 
defaultActions previewActions: [WKPreviewActionItem]) -> UIViewController?
public func webView(_ webView: WKWebView,  
commitPreviewingViewController previewingViewController: UIViewController)

Peek & Pop
Bring your own UI!
UIPreviewInteraction
UIKit provides the “feel” of Peek & Pop
func previewInteraction(_ previewInteraction: UIPreviewInteraction,
                        didUpdatePreviewTransition transitionProgress: CGFloat, ended: Bool) {
   self.updateUIToPeek(transitionProgress)
   if ended {
      self.showPeekUI()
   }
}


Collection View
Automatic self-sizing cells  in flow layout
Paging support in collection   view reordering


Collection View
Smooth scrolling
Cell prefetching
Data prefetching
(also available in UITableView)



Advances in UIKit Animations
UIViewPropertyAnimator
Interruptible Scrubbable Reversible
Rich timing features Dynamic


Advances in UIKit Animations
let timing = UICubicTimingParameters(animationCurve: .easeInOut) 
let animator = UIViewPropertyAnimator(duration: duration, timingParameters: timing)
animator.addAnimations { 
self.squareView.center = CGPoint(x: point.x, y: point.y) 
}
animator.startAnimation()
Advances in UIKit Animations and Transitions

