# [2017 607 Metal 2 Optimization and Debugging](https://developer.apple.com/videos/play/wwdc2017/607/)



- Seth Sowerby, GPU Software
- Max Christ, GPU Software
- Jose Enrique D'Arnaude del Castillo, GPU Software

### Metal 2

- GPU-driven rendering
- Platform feature alignment
- Machine Learning acceleration
- VR (macOS)
- External GPU support (macOS)
- __Advanced optimization tools__


Metal 2 Developer Tools

- Metal tools recap
- Metal frame debugger enhancements
- New GPU profiling tools


•Metal Frame Debugger
• Pulling your frame apart, bit by bit



Metal Frame Debugger

The story so far

- Fully featured frame debugger
- Navigate through your workload
- Inspect state and resource
- Debug graphics and compute
- Integrated into Xcode

Full Metal 2 Support

- Raster order groups
- Sampler arrays
- Viewport arrays
- New pixel formats
- New vertex array formats


### Full Metal 2 Support

Argument buffers


### VR Support

- Automatic support for SteamVR
- View submitted surfaces in stereo

Improved Capture Workflow
Enhanced support for advanced workloads New lightweight capture API
Capture the exact workload you’re interested in Group workload into logical scopes
Trigger capture programmatically


### Metal Quick Looks

- Lightweight Metal debugging in the   CPU Debugger
- View textures, buffers and samplers inline
- Use when the frame debugger is too invasive
- Resource loading and setup code


### Advanced Filtering (NEW)

- Improved navigation and data mining for complex scenes
- Autocomplete suggestions Compound terms



### Pixel Inspection
Finally!

- Detailed inspection of individual pixels
- Simultaneously inspect multiple attachments
- Examine image elements in compute workloads

NEW
 

### Inspect Vertex Attribute Outputs

- Inspect output of your vertex shaders
- Shown inline with vertex attribute inputs

NEW
 

## Demo|Max Christ

## GPU Profiling

Finding the nano-second

### Profile, Optimize, Repeat - Always nano-seconds to be found


- Performance is crucial to games
- Consistent fast frame rate
- Get the most out of the GPU for the best looking game
- Increase efficiency for longer gaming experience
- Use the GPU profiling tools


### Metal System Trace

Investigate timing issues
CPU/GPU parallelism Frame rate stutters
Trace your Metal workloads through the system

CPU to GPU to Display


Integrated into Instruments


....



## Demo|Jose Enrique D'Arnaude del Castillo|


