## [Using Core Image with Vision](6-using-core-image-with-vision.md) | David, Sky | 3930 | p177


### Using Core Image with Vision

Direction|Use case|Example
--|--|--
CI-VN| Core Image can prepare images before being passed to Vision|Cropping, Orienting, Converting to grayscale
VN-CI|Vision can gather information before processing with Core Image| Feature detection can guide which CIFilters to apply


### Photo from Video with Removal of Unwanted Objects

Step|Framework|Task
--|--|--
1|AVFoundation| Get the frames out of a short video
2|Vision| Determine homography matrices to align frames
3|Core Image| Align each video frame
4|Core Image| Make a photo from the median of the aligned frames


### // 1. Use Vision to find homographic registration and pass it to CI (p190)

```swift
func homographicTransform(from image: CIImage, to reference: CIImage) -> matrix_float3x3? {
  // Create the request and request handler
  let request = VNHomographicImageRegistrationRequest(targetedCIImage: image)
  let requestHandler = VNImageRequestHandler(ciImage: reference, options: [:])
  // Send the request to the handler
  try? requestHandler.perform([request]);
  // Get the observation
  guard let results = request.results,
    let observation = results.first as? VNImageHomographicAlignmentObservation
  else {
        return nil
  }
  return observation.warpTransform
}
```

### // 2. Core Image Metal kernel to apply a homography matrix p195

```swift
float2 warpHomography(float3x3 h, destination dest) {
  float3 homogeneousDestCoord = float3(dest.coord(), 1.0);
  float3 homogeneousSrcCoord = h * homogeneousDestCoord;
  float2 srcCoord = homogeneousSrcCoord.xy / max(homogeneousSrcCoord.z, 0.000001);
  return srcCoord;
}
```

## // 4. Core Image Metal kernel to return the median of 5 images

```swift
inline void swap(thread float4 &a, thread float4 &b) {
  float4 tmp = a; a = min(a,b); b = max(tmp, b); // swap sort of two elements
}

float4 medianReduction5(sample_t v0, sample_t v1, sample_t v2, sample_t v3, sample_t v4) {
  // using a Bose-Nelson sorting network
  swap(v0, v1); swap(v3, v4); swap(v2, v4); swap(v2, v3); swap(v0, v3);
  swap(v0, v2); swap(v1, v4); swap(v1, v3); swap(v1, v2);
  return v2;
}
```

## Demo : Photo from Video with Removal of Unwanted Objects |Sky Gao, Image Engineer | 4430

We have a homographic line, and which David just mentioned, but Vision also offers a translational alignment which, in this case, doesn't work extremely well.

So what we do here instead is we take the median of median as an approximation.
