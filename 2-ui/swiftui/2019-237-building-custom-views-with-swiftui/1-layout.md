
### Layout Basics

See [Apple Dev Doc: View Layout](https://developer.apple.com/documentation/swiftui/view/layout)

### Layout Procedure


1. Parent proposes a size for child
2. Child chooses its own size
3. Parent places child in parent’s coordinate space
4. SwiftUI rounds coordinates to nearest pixel


.frame(width: 50, height: 10)

.aspectRatio(1)


### Delicious Avocado Toast

```swift
struct Toast : View {
    var body: some View {
        Text("Avocado Toast")
            .padding(10) // or [.leading, .trailing]
            .background(Color.green)
    }
}
```

### Scrumptious Avocado

```swift
struct Avocado : View {
    var body: some View {
        Image("20x20_avocado")
            .frame(width: 30, height: 30)
    }
}
```


The frame is not contraint in SwiftUI, it is just the view

### This Is as It Should Be

There’s no wrong way to do it

### [HStack](https://developer.apple.com/documentation/swiftui/hstack) and [VStack](https://developer.apple.com/documentation/swiftui/vstack)


### Layout Priority

```swift
Text("Avocado Toast").layoutPriority(1)
```


### Alignments

```swift
HStack(alignment: .lastTextBaseline) {
    Text("Delicious").font(.caption)
    Image("20x20_avocado")
        .alignmentGuide(.lastTextBaseline) { d in d[.bottom] * 0.927 }
    Text("Avocado Toast").layoutPriority(1)
}
.lineLimit(1)
```
See struct [`ViewDimensions`](https://developer.apple.com/documentation/swiftui/viewdimensions)

### Defining a New Vertical Alignment ()

```swift
extension VerticalAlignment {
    private enum MidStarAndTitle : AlignmentID {
        static func defaultValue(in d: ViewDimensions) -> Length {
        return d[.bottom]
        }
    }
    static let midStarAndTitle = VerticalAlignment(MidStarAndTitle.self)
}
```

see protocol [`AlignmentID`](https://developer.apple.com/documentation/swiftui/alignmentid)

### Using the New Vertical Alignment

```swift
HStack(alignment: .midStarAndTitle) {

    Text("★★★★★")
        .alignmentGuide(.midStarAndTitle) { d in d[.bottom] / 2 }

```
