
## [MetalKit](607-1-metalkit.md) | Dan Omachi | 214

Utility functionality for Metal Apps

MetalKit View Setup
Approaches to using MTKView
A. Implement a delegate
```
    - (void)drawInView:(MTKView *)view
    - (void)view:(MTKView *)view willLayoutWithSize:(CGSize)size
```

B. Subclass MTKView
iOS
    - (void)drawRect:(CGRect)rect
    - (void)layoutSubviews
OS X
    - (void)drawRect:(CGRect)rect
    - (void)setFrameSize:(NSSize)newSize
