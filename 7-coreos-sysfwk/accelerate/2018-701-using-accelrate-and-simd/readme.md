# [2018 701 Using Accelerate and simd](https://developer.apple.com/videos/play/wwdc2018/701)

2018-701-using-accelrate-and-simd.md

Learn how to use sophisticated Signal and Image Processing techniques to bring higher performance to your apps while lowering battery consumption. See compelling use cases for the Accelerate framework with interactive demos. Explore using simd—a valuable addition that effortlessly brings vector programming to your apps.

Length: 36:48

Speakers

- Matthew Badin, CoreOS, Vector and Numerics 
- Luke Chang, CoreOS, Vector and Numerics

TOC 

Topic|Speaker|Time|Page
---|---|---|---
Accelerate (Overview)|Matthew Badin|1:30|p3
[vDSP](1-vdsp.md) | Matthew Badin |3:30|
[simd](2-simd.md) | Matthew Badin | 1240 | p22
[vImage](3-vimage.md)  | Luke Chang | 1930 
LINPACK Benchmark |Luke Chang | 3200 |


### Composition of Accelerate Framework

X|Y
---|---
vDSP|Signal processing
vImage|Image processing
vForce|Vector transcendental functions
BLAS, LAPACK, LinearAlgebra|Dense matrix computations Sparse BLAS, Sparse Solvers|Sparse matrix computations 
BNNS|Neural networks


### Closely Related

X|Y
---|---
simd|Small vector and matrix computation for CPU 
Compression|Lossless data compression


## LINPACK Benchmark  | 3200 

How fast can you solve a system of equations? 

Actually three separate benchmarks:

- 100-by-100 system 
- 1000-by-1000 system
- “No holds barred”

## Summary

- Wide varieties of functionalities
- Easy to use
- Fast and energy efficient
- Portable across platforms and architectures