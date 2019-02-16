# [Creating 3D models for AR Quick Look](3-creating-3d-models-for-ar-quick-look.md)|2000|p27


## Creating 3D Models for AR Quick Look


### Creating 3D Models

- Placement
- Physical size
- Animation
- Contact shadow
- Appearance
- Transparency

Optimizing and exporting models

### Placement

- Place objects facing towards the camera (facing +z)
- Base of object should sit on the ground plane (y = 0)
- Pivot point should be at the origin (x, y, z = 0)

### Animation

- Provide an “idle” animation to add life to the object
- Animations always loop
- Animations can be a mix of skeletal animation and transform animation


### Animation Tips

- Choose animations that enhance AR immersiveness
- Don’t animate objects away from the origin
- Keep a consistent bounding box throughout an animation
- Prefer animations that make sense at a static location
- Or create animations as self-contained scenes


### Contact Shadow

- AR Quick Look provides a contact shadow for you
- Can turn the shadow on and off
- Can apply ambient lighting conditions
- Don’t bake a contact shadow into the model
- First animation frame is used for shadow creation

### Model Appearance

- AR Quick Look uses a Physically Based Rendering (PBR) shader
  - Albedo (base color)
  - Metallic (conductor or insulator)
  - Roughness (rough or shiny)
  - Normal (surface details)
  - Ambient occlusion (internal shadows)
  - Emissive (emits light)

[2018 Creating Great AR Experiences]


### Transparency

- Use a separate material for transparent and non-transparent parts of the model
- Provide an albedo texture with transparency in its alpha channel
- Use transparency for see-through areas, not for cutouts


### Texture Formats

- Albedo (RGB/RGBA)
- Metallic (Grayscale)
- Roughness (Grayscale)
- Normal (RGB)
- Ambient occlusion (Grayscale)
- Emissive (RGB)
- Any image format supported by iOS
- Textures should be square powers of 2 (2048, 1024, 512...)

### Supporting All Devices

- System-wide extension that shares system memory with applications
- Optimize and test your models for high-memory devices
  - iPhone 7 Plus, iPhone 8 Plus, iPhone X
  - iPad Pro 12.9”
- AR Quick Look will dynamically downsample textures for other devices   when needed
- Meshes and animations are not modified

### Size Limits

- Many factors affect a model’s memory requirements
  - Mesh and animation complexity
  - Texture size and count 
- As a guide, for a model with a single PBR material
  - 100k polygons
  - One set of 2048 by 2048 PBR textures
  - Ten seconds of animation
- Always test your model on a real device

### Optimizing Models

- Freeze transforms and merge adjacent vertices
- If possible, use a single material/texture set for the entire model
- Don’t include textures you don’t need
- Spend your texture budget on areas that add most value and realism
- Remember that pixels have a physical size in AR
- Balance texture size and quality against download size


### ‘usdz’ Converter

- Command line tool to convert 3D models  to .usdz format
- Ships with Xcode 10
- Maps PBR textures to meshes and submeshes
- Input formats
  - OBJ file
  - Single-frame Alembic (ABC) file
  - USD file (either .usda or .usdc)

### Anatomy of a ‘usdz’ File

- A .usdz file is an uncompressed zip archive
- First file in the archive is a .usdc file (model, animation, material definitions)
- Remaining files (if needed) are image files

```
// Call usdz_converter with xcrun.
 xcrun usdz_converter RetroTV.obj RetroTV.usdz
// PBR textures can be applied to groups (meshes and submeshes) with the -g option.
xcrun usdz_converter RetroTV.obj RetroTV.usdz
-g RetroTVMesh
-color_map RetroTV_Albedo.png
-metallic_map RetroTV_Metallic.png
-roughness_map RetroTV_Roughness.png
-normal_map RetroTV_Normal.png
-ao_map RetroTV_AmbientOcclusion.png
-emissive_map RetroTV_Emissive.png
 
// Use the -v option to print out group names and other verbose information during conversion.
xcrun usdz_converter RetroTV.obj RetroTV.usdz -v

```

https://developer.apple.com/arkit/gallery/


