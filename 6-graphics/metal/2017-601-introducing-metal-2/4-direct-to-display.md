

## Direct to Display | 3950 | p121



### Direct to Display Requirements

- Opaque Layer
- No masking, rounded corners, and so on
- Full screen (or with “black bars” via an opaque black background color)
- Dimensions matching the display or smaller
- Color Space and Pixel Format compatible with the display


### Colorspace Requirements

### Detecting P3 Display Gamut

UIKit
UITraitCollection.displayGamut == .P3
AppKit
NSScreen.canRepresent(.p3)

### Summary

- Eliminate compositor usage of GPU
- Useful for full-screen scenes
- Supported on iOS, tvOS, and macOS
- Use Metal System Trace to verify