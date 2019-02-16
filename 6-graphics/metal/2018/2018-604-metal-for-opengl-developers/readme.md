

# [Metal for OpenGL Developers](https://developer.apple.com/videos/play/wwdc2018/604/)


2018-604-metal-for-opengl-developers/readme.md



## •Metal Porting | p111


- Build 
  - Shaders
- Initialize
  - Devices and Queues
  - Render Objects
- Render
  - Command Buffers
  - Resource Updates
  - Render Encoders
  - Display


### Metal Shading Language

- Based on C++
  - Classes, templates, structs, enums, namespaces
- Built-in types for vectors and matrices
- Built-in functions and operators
- Built-in classes for textures and samplers


### Shader Compilation - Building with Xcode

- Xcode compiles shaders into a Metal library (.metallib)
- Front-end compilation to binary intermediate representation
- Avoids parsing time on customer systems
- By default, all shaders built into default.metallib
  - Placed in app bundle for run time retrieval


3420 