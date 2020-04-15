

## [2019 216 SwiftUI Essentials](https://developer.apple.com//videos/play/wwdc2019/216/)


- Matt Ricketson, SwiftUI Engineer
- Taylor Kelly, SwiftUI Engineer


Topic|x
--|--
Getting Started: Views and modifiers|
Building custom views|p86
Composing Controls|p148
Navigating your app|p257



```swift
Form 

SectionHeader

```




Imperative Avocado Toast


Declarative Avocado Toast

“I’d like some avocado toast on charred sourdough with almond butter, sea salt, and red pepper flakes.”
“Oh, and cut it diagonally.”


View Container Syntax


```swift
public struct VStack<Content : View> : View {   
    public init(
        alignment: HorizontalAlignment = .center, 
        spacing: Length? = nil,
        @ViewBuilder content: () -> Content
    ) 
}
```



Binding Syntax

```swift
struct OrderForm : View {
    @State private var order: Order
    var body: some View {
        Stepper(value: $order.quantity, in: 1...10) {
            Text("Quantity: \(order.quantity)") 
        }
    } 
}
```


Prefer smaller, single-purpose views


Build larger views using composition



## Building custom views|p86

Views Using Modifiers

Primitive Views

```swift
AppIcon()
.rotationEffect(.degrees(flipped ? 180 : 0))

```

Form

Button


Adaptive Controls

Toggle

Picker

ForEach

Controls in SwiftUI

Control Modifiers


Environment


## Navigating your app|p257



```swift

```


