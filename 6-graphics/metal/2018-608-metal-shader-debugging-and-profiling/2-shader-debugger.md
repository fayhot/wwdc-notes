
## [Debugging Shaders with Shader Debugger](2-shader-debugger.md)


Shader Debugging

- Math heavy code
- Highly parallel
- Unity’s “Book of the Dead”

- ~10 million vertex shader invocations
- ~60 million pixels rendered

Shader Debugger

New tool for debugging Metal shaders
Rich variable visualization across thousands of threads
Real data from GPU
Flexible stepping
Integrated into Metal Frame Debugger


## Demo - Xavier Verguin Gonzalez



### Inspecting Variables

- Just go the source line
- The side bar for the modified variables Details view for full information
- Hover for in place access
- Variables view for variables in scope


### Following the Execution

- All source lines executed are available in navigator
- Flexible stepping Backwards debugging
- Use filter to focus



### Access to Other Threads

Set of threads are available based on the initial selection

- Vertex — Primitive of the selected vertex
- Fragment — Rectangle around the selected pixel
- Compute — Threadgroup of the selected thread

### Comparing Good and Bad Pixels

- Quickly compare threads
- Execution history and  variables are updated for   the selected thread


## Demo - Xavier Verguin Gonzalez

