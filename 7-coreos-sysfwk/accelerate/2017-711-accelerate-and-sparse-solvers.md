# [2017 711 Accelerate and Sparse Solvers](https://developer.apple.com/videos/play/wwdc2017/711/)

- Accelerate
- Compression
- Basic Neural Network Subroutines
- The simd Module
- Sparse Matrices

## Accelerate

- vImage—image processing
- vDSP—signal processing
- vForce—vector functions
- BLAS, LAPACK, LinearAlgebra—dense matrix computations
- Sparse BLAS, Sparse Solvers—sparse matrix computations
- BNNS—neural networks
- simd—types and functions for CPU vector units
- Compression—lossless data compression



BNNSFilterCreateConvolutionLayer
BNNSFilterApply


Benefits
2,800 APIs Less code Faster
Energy efficient All architectures


## Compression | 700


## Basic Neural Network Subroutines | 840

## The simd Module | 1140 | p38

```

// Simplified vector programming
#include <simd/simd.h>

/*! @abstract Evaluates the logistic curve with specified `midpoint` and `maximumSlope`. */
simd_float16 logistic(simd_float16 x, float midpoint, float maximumSlope) {
  simd_float16 linear = -maximumSlope*(x - midpoint);
  simd_float16 exponential = exp(linear);
  return 1/(1+ exponential);
}
```


### Quaternions

Quaternions extend the complex numbers like complex numbers extend the reals


Unit Quaternions
Quaternions with length 1 are called unit quaternions
Unit complex numbers can represent rotations in two dimensions Unit quaternions can represent rotations in three dimensions

```
// Quaternions as Rotations
import simd
// A vector
let v = float3(1,1,0)
// Quaternion that rotates by π/2 radians about the y axis.
let q = simd_quatf(Float.pi/2, [0,1,0]) let u = simd_act(q,v)
```


## BLAS, LAPACK | 2130


## Sparse Matrices | 2240 | p79

```
// Defining a sparse matrix
#include <Accelerate/Accelerate.h>

long columnStarts[] = { 0, 3, 7, 9 };
introwIndices[] ={ 0, 1, 3, 0, 1, 2, 3, 1, 2 };
float values[] = { 2.0, -0.2, 2.5, 1.0, 3.2, -0.1, 1.1, 1.4, 0.5 };



SparseMatrix_Float A = { .structure = {
.attributes = { .type = SparseOrdinary }, .rowCount = 4,
.columnCount =3,
.blockSize = 1,
.columnStarts = columnStarts,
.rowIndices = rowIndices },
.data = values };


```

- 1) Matrix factorization
  - Simple
  - Accurate
- 2) Iterative methods
  - Faster for huge matrices
  - Problem-specific preconditioner


x

```
long columnStarts[] = { 0, 3, 6, 7, 8};
int rowIndices[] ={ 0, 1, 3, 1, 2, 3, 2, 3};
float values[] = { 10.0, 1.0, 2.5, 12.0, -0.3, 1.1, 9.5, 6.0 };

SparseMatrix_Float A = {
 .structure = {
    .attributes = {
      .kind = SparseSymmetric,
      .triangle = SparseLowerTriangle
},
// ...
}, };
```



### What if A is Not Square?  - Least Squares Solutions


Underdetermined

min ||x||2 st Ax = b

```

status = SparseSolve(SparseConjugateGradient(), A, b, x, SparsePreconditionerDiagonal);


status = SparseSolve(SparseLSMR(), A, b, x, SparsePreconditionerDiagScaling);
```
