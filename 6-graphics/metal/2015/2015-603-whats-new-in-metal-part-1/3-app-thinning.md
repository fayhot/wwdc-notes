
## [Metal and App Thinning](3-app-thinning.md) | 2920 | p146


Capability Matrix

X|512MB|1GB|2GB
---|---|---|---
Metal GPUFamily2||512x512 ASTC|1024x1024 ASTC
Metal GPUFamily1||512x512 EAC
OpenGL ES Legacy|256x256 RG8|512x512 RG8




### Xcode 


### Custom Tools Pipelines



- Publicly documented JSON file format
- Easily integrated into custom toolchain


### Retrieving Named Data
NSDataAsset class provides correctly matched data resource from Asset Catalog

```objc
    #import <UIKIt/NSDataAsset.h>
    NSDataAsset *asset = [[NSDataAsset alloc] initWithName:@“NormalMaps”];
    NSData *data = asset.data;
```

