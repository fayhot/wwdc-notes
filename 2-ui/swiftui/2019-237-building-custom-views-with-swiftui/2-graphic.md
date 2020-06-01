
## Graphics in SwiftUI - by John Harper - 23:15

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

```swift
struct WedgeShape: Shape {
    var wedge: Ring.Wedge
    func path(in rect: CGRect) -> Path {
        var p = Path()
        let g = WedgeGeometry(wedge, in: rect)
        p.addArc(center: g.cen, radius: g.r0, startAngle: g.a0, endAngle: g.a1, clockwise: false) p.addLine(to: g.topRight)
        p.addArc(center: g.cen, radius: g.r1, startAngle: g.a1, endAngle: g.a0, clockwise: true)
        p.closeSubpath()
        return p
    }
}
```

Multi-Part Drawing


### [ZStack](https://developer.apple.com/documentation/swiftui/zstack)

```swift
struct RingView: View {
    var body: some View {
        ZStack {
            ForEach(ring.wedgeIDs) { id in
                WedgeView(self.ring.wedges[id]!)
                    .tapAction { withAnimation { self.ring.deleteWedge(id: id) } }
                    .transition(scaleAndFade)
            }
        }
    }
}
```


### Custom Transitions

```swift
struct ScaleAndFade: ViewModifier {
    var isActive: Bool

    func body(content: Content) -> some View {
        return content
            .scaleEffect(isActive ? 0.1 : 1) // scale: 10% or 100%
            .opacity(isActive ? 0 : 1) // opacity: 0% or 100%
    }
}

let scaleAndFade = AnyTransition.modifier(
    active: ScaleAndFade(isActive: true),
    identity: ScaleAndFade(isActive: false))
```

### Demo


### Graphic Effects

- Opacity
- Geometry (scales, rotations, etc.)
- Color effects (contrast, brightness, hue rotate, monochrome, etc.)
- Blur effect
- Drop shadow effect
- Clipping, masking
- Compositing, groups, blend modes


