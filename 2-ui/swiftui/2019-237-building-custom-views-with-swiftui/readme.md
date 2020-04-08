
## [2019 237 Building Custom Views with SwiftUI](https://developer.apple.com/videos/play/wwdc2019/237/)


### Layout Basics


### Layout Procedure


1. Parentproposesasizeforchild
2. Child chooses its own size
3. Parent places child in parent’s coordinate space
4. SwiftUI rounds coordinates to nearest pixel


.frame(width: 50, height: 10)

.aspectRatio(1)


### Delicious Avocado Toast


### Scrumptious Avocado

The frame is not contraint in SwiftUI, it is jsut the view


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


Defining a New Vertical Alignment
 
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

Using the New Vertical Alignment

```swift
HStack(alignment: .midStarAndTitle) {

    Text("★★★★★")
        .alignmentGuide(.midStarAndTitle) { d in d[.bottom] / 2 }

```

## Graphics in SwiftUI - by John Harper

Drawing ↔ Views

regular views and graphic views


### Drawing Model

shape.op(style) → view

- fill
- stroke
- strokeBorder

### Shape Styles

Styles are ways of making a view from a shape

- Colors
- Tiled images
- Gradients: Linear, radial, angular (conic)


### Gradients

```swift
struct GradientView: View { 
    var body: some View {
        let spectrum = Gradient(colors: [
            .red, .yellow, .green, .cyan, .blue, .purple, .red
        ])
        let conic = AngularGradient(gradient: spectrum, center: .center, angle: .degrees(-90))
        return Circle().strokeBorder(conic, lineWidth: 50) 
    }
}
```


### Wedge


### [ZStack](https://developer.apple.com/documentation/swiftui/zstack)


### Custom Transitions




### Graphic Effects

- Opacity
- Geometry (scales, rotations, etc.)
- Color effects (contrast, brightness, hue rotate, monochrome, etc.) 
- Blur effect
- Drop shadow effect
- Clipping, masking
- Compositing, groups, blend modes




### SwiftUI’s Unified Model

All customization centers on View

- Layout
- Graphics
- Animation and transitions
- Interaction

Combine these to produce delightful results!