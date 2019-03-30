

# [2018 608 Metal Shader Debugging and Profiling](https://developer.apple.com/videos/play/wwdc2018/608/)

- Metal Frame Debugger
- Step through API calls
- Resource inspection
- Shader edit and reload GPU counters
- Pipeline statistics Integrated into Xcode

NEW

- Dependency viewer
- Geometry viewer
- Shader debugger
- Enhanced shader profiler
 
### TOC: 3 tools



## [Geometry Viewer](1-geometry-viewer.md)

Visualize the post-vertex transform data in 3D Access to all vertex data
Per-draw call view



### Visibly Wrong Triangles


### Out of Frustum Objects


### Missing Triangles



## Optimizing Shaders with Shader Profiler | | p78

Knowing What to Optimize
Profiling tools built into Metal Frame Debugger

- GPU counters
- Pipeline statistics
- Shader profiler


### Shader Profiler

- Provides per-pipeline timing information
- Per-line execution cost (iOS and tvOS)
- Shader edit and reload
- Get into shader debugger

### Enhanced Shader Profiler for A11

Instruction category cost breakdown per line

- ALU — Float, half, and complex
- Memory — Sample, load, and store operations
- Synchronization — Wait memory, barriers, or atomics

Visibility into inline function cost


## Demo | Max Christ | | p92


### Access to Shader Sources

New Metal Compiler option Xcode project


  “Yes, include source code”

from build settings

Command line

“-MO” compiler option
