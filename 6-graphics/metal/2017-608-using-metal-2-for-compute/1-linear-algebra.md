
## [Linear Algebra](1-linear-algebra.md) | 250 | p9

New primitives

- Matrix-Matrix Multiplication
- Matrix-Vector Multiplication
- Triangular Matrix Factorization and Linear Solvers


### Data Representations

class|brief|iOS
---|---|---
[`MPSVector`](https://developer.apple.com/documentation/metalperformanceshaders/mpsvector)|Interprets data in MTLBuffer as a 1-dimensional array|11
[`MPSMatrix`](https://developer.apple.com/documentation/metalperformanceshaders/mpsmatrix)|Interprets data in MTLBuffer as a rectangular array<br/>Row-major order|10
[`MPSTemporaryMatrix`](https://developer.apple.com/documentation/metalperformanceshaders/mpstemporarymatrix)|Allocated from MTLHeap<br/>Use for most of your intermediate matrices|11


### MPSVector and MPSMatrix - Input types

- Single Precision Floating-Point
- Half Precision Floating-Point
- 16-bit Signed Integer
- 8-bit Signed Integer

### MPSVector - Code example

Create a vector of size N

```swift
// Create a Metal buffer of length N
let buffer = device.makeBuffer(length: N * MemoryLayout<Float32>.size)
// Create a vector descriptor
let descriptor = MPSVectorDescriptor(length: N, dataType: .float32)
// Create a vector with descriptor
let vector = MPSVector(buffer: buffer, descriptor: descriptor)
```

### MPSMatrix - Code example

Create a matrix with M rows and N columns

```swift
// Get the recommended bytes per row value to use for sizing a Metal buffer
let bytesPerRow = MPSMatrixDescriptor.rowBytes(forColumns: N, dataType: .float32) 
// Create a Metal buffer with the recommended bytes per row
let buffer = device.makeBuffer(length: M * bytesPerRow)
// Create a matrix descriptor
let descriptor = MPSMatrixDescriptor(rows: M, columns: N, rowBytes: bytesPerRow, dataType: .float32)
// Create a matrix with descriptor
let matrix = MPSMatrix(buffer: buffer, descriptor: descriptor)
```

Primitives

- Matrix-Matrix and Matrix-Vector Multiplication
  - API modeled after standard BLAS GEMM and GEMV interfaces
- Triangular Matrix Factorization and Linear Solvers
  - API modeled after standard LAPACK decomposition and solve interfaces


### // Example: Matrix-Matrix Multiply: C = A B

```swift

// Create matrices A, B and C
let A = MPSMatrix(buffer: ABuffer,
    descriptor: MPSMatrixDescriptor(rows: M, columns: K,
        rowBytes: ARowBytes, dataType: .float32))

let B = MPSMatrix(buffer: BBuffer,
    descriptor: MPSMatrixDescriptor(rows: K, columns: N,
        rowBytes: BRowBytes, dataType: .float32))

let C = MPSMatrix(buffer: CBuffer,
    descriptor: MPSMatrixDescriptor(rows: M, columns: N,
        rowBytes: CRowBytes, dataType: .float32))

```

### // Example: Matrix-Matrix Multiply: C = A B


```swift
// Perform Metal setup
let device = MTLCreateSystemDefaultDevice()!
let commandQueue = device.makeCommandQueue()
let commandBuffer = commandQueue.makeCommandBuffer()

// Create a Matrix-Matrix Multiplication kernel
let mmKernel = MPSMatrixMultiplication(device: device, resultRows: M,
resultColumns: N, interiorColumns: K)

// Encode kernel to the command buffer
mmKernel.encode(commandBuffer: commandBuffer, leftMatrix: A,
rightMatrix: B, resultMatrix: C)

// Tell GPU to start doing the work
commandBuffer.commit()
```

### Sample Code

- MPSMatrixMultiplication
  - https://developer.apple.com/library/content/samplecode/MPSMatrixMultiplicationSample
- Triangular Matrix Factorization and Linear Solvers
  - Coming soon

