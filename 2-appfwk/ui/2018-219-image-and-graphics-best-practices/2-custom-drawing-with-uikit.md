## [Custom drawing with UIKit](2-custom-drawing-with-uikit.md) | 2200| p72



### Custom Drawing Versus UIImageView




### Backing Store Memory Costs

- Proportional to pixel size of view
- Element size grows to accommodate color range used by drawing
- Setting CALayer.contentsFormat opts out
- Update layerWillDraw(_:) implementations

### Reducing Backing Store Use

- Refactor larger views into subview hierarchies
- Reduce or eliminate overrides of draw(_:)
- Eliminate duplicate copies of image data
- Use optimized view properties and subclasses

### Reducing Backing Store Use - Alternatives to custom drawing

- Overriding draw(_:) opts into backing store
- UIView.backgroundColor can render directly to frame buffer without a backing store
  - ...except for pattern colors
  - Use UIImageView with tiling image instead

### Reducing Backing Store Use - Masking versus corner radius

- UIView.maskView and CALayer.maskLayer render view hierarchy into temporary image buffer
- CALayer.cornerRadius does not require any image buffer
- Consider UIImageView with resizable image instead of masking for transparent backgrounds

### Reducing Backing Store Use - Eliminating duplicate image data

- UIImageView can colorize monochrome images while rendering directly into frame buffer
- UIImage.withRenderingMode(_:) or Rendering Mode popup in asset inspector
- Set tintColor of image view to any solid color

### Reducing Backing Store Use - UILabel optimizations for rendering text

- UILabel is optimized for monochrome strings
- Uses 75% smaller backing store when possible
- Automatically upgrades to larger backing store for multicolor strings, emoji

### Drawing Off-Screen - Optimizing image buffers - NEW

- Similar automatic Wide Color support as backing stores
- Prior to iOS 12 and tvOS 12, defaults to Wide Color support based on hardware
- Set prefersExtendedRange on UIGraphicsImageRendererFormat for direct control 
- UIImage.imageRendererFormat may offer an intermediate representation


## Advanced CPU and GPU techniques|3030|p97


### Advanced Image Effects - Core Image

- Consider Core Image for realtime effects
- Executes on GPU, freeing up CPU
- UIImageView renders CIImages efficiently
- UIImage.init(ciImage:)
 

### Advanced Image Processing - Interfacing with other frameworks

- Use CVPixelBuffer to move data to frameworks like Metal, Vision, and Accelerate
- Use the best initializer—don’t unwind work that’s already been done
- Guard against moving work between GPU and CPU
- Ensure buffers are correct format for Accelerate

