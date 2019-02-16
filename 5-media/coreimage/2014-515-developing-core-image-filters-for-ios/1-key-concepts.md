

## [Key Concepts](1-key-concepts.md) | |

Intermediate images are lightweight objects


### Core Image Classes

* CIKernel
  * Represents a program written in Core Image’s kernel language
* CIFilter
  * Has mutable input parameters
  * Uses one or more CIKernels to make a new image based on inputs
* CIImage
  * An immutable object that represents the recipe for an image Non zero origin (lower left) and possibly infinite bounds
* CIContext
  * A object through which Core Image draws results


### Starting assumptions


### Workflow -  Using Core Image on iOS
Create input CIImages
Subclass CIFilter   
 •  •
Get output CIImage
Use CIContext to render output image (to CGImageRef, EAGL context, etc.)


### 115 Built-in CIFilters on iOS (27 Warps)



### Anatomy of CIKernel

``` objectivec
@interface CIKernel  
+ (CIKernel *) kernelWithString:(NSString *);
- (CIImage *) applyWithExtent:(CGRect)extent
                 roiCallback:(CIKernelROICallback)callback
                 arguments:(NSArray *)arguments;
@end
GLSL + extensions for imaging Inputs and outputs are floats
```
