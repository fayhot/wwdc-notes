## [simd](2-simd.md) | Matthew Badin | 1240 | p22

The simd Module

- Simplified vector programming
- Small (fixed-size) vector and matrices
- Abstract architecture-specific types and instrinsics


### // Average Two Vectors (Positive)

```swift
let x = simd_float4(1,2,3,4) 
let y = simd_float4(3,3,3,3)
let z = 0.5 * (x + y)
```

### simd

- Matrices of size 2, 3, or 4 and vectors of 2, 3, 4, 8, 16, 32, or 64
- Arithmetic operators (+,-,*,/) work with both vectors and scalars
- Supports common vector math and geometry operations (dot, length, clamp)
- Support for transcendental functions
- Quaternions

### Quaternions

```swift
// Vector to Rotate
let original = simd_float3(0,0,1)

// Axis of Rotation
let quaternion = simd_quatf(
    angle: .pi / -3,
    axis: simd_float3(1,0,0))

// Apply the Rotation
let rotatedVector = simd_act(quaternion, original)
```


### multiple axes 

```swift 
// Vector to Rotate
let original = simd_float3(0,0,1)

// Axis of Rotation
let quaternion = simd_quatf(angle: .pi / -3,
    axis: simd_float3(1,0,0))
 
let quaternion2 = simd_quatf(angle: .pi / 3,
    axis: simd_float3(0,1,0))

// Combine the Two Rotations
let quaternion3 = quaternion2 * quaternion

// Apply the Rotation
let rotatedVector = simd_act(quaternion3, original)
```

### // Slerp Interpolation

```swift
let blue = simd_quatf(...) 
let green = simd_quatf(...) 
let red = simd_quatf(...)

for t: Float in stride(from: 0, to: 1, by: 0.001) {
    let q = simd_slerp(blue, green, t)
    // Code to Add Line Segment at `q.act(original)`
}

for t: Float in stride(from: 0, to: 1, by: 0.001) {
    let q = simd_slerp_longest(green, red, t)
    // Code to Add Line Segment at `q.act(original)`
}
```

### // Spline Interpolation

```swift 
let original = simd_float3(0,0,1)
let rotations: [simd_quatf] = ...

for i in 1 ... rotations.count - 3 {
    for t: Float in stride(from: 0, to: 1, by: 0.001) {
        let q = simd_spline(
            rotations[i - 1], // previous
            rotations[i],
            rotations[i + 1], 
            rotations[i + 2], // next
            t)
        // Code to Add Line Segment at `q.act(original)`
    }
}
```

### Animation Comparson between Slerp and Spline

Sample Code: [Rotating a Cube by Transforming Its Vertices](https://developer.apple.com/documentation/accelerate/simd/rotating_a_cube_by_transforming_its_vertices)