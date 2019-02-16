
## [System Broadcast Picker](2-system-broadcast-picker.md) | 835 | p22

### Broadcast Picker

- Your app can initiate an iOS system broadcast session
- Simple one-button UI
- No compromises for privacy
- Secure architecture
- New in iOS 12


### // RPSystemBroadcastPickerView

```swift
import ReplayKit.broadcast
class ViewController: UIViewController {
    var broadcastPicker: RPSystemBroadcastPickerView?
 
    override func viewDidLoad() {
        super.viewDidLoad()
        broadcastPicker = RPSystemBroadcastPickerView(frame: kPickerFrame)
        view.addSubview(broadcastPicker)
    }
}
```

preferredExtension
Pairs broadcast picker to a particular extension Assign bundle identifier of your extension Initialize before view is presented


```swift
import ReplayKit.broadcast
class ViewController: UIViewController {
var broadcastPicker: RPSystemBroadcastPickerView?
 
override func viewDidLoad() {
super.viewDidLoad()
broadcastPicker = RPSystemBroadcastPickerView(frame: kPickerFrame)
broadcastPicker.preferredExtension = “com.your-app.broadcast.extension”
 }
view.addSubview(broadcastPicker)

```