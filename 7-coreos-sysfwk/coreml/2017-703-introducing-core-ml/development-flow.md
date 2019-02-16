
## Development Flow

### Getting the Model


### Demo Recap - Image based flower identifier


Xcode integration

### Simple usage

```swift
let flowerModel = FlowerClassifier()
if let prediction = try? flowerModel.prediction(flowerImage: image) {
  return prediction.flowerType
}
```

Type of model abstracted

Input/output strongly typed

### Generated Source
```swift
class FlowerClassifierInput { var flowerImage: CVPixelBuffer

}
class FlowerClassifierOutput {
  let flowerType: String
  let flowerTypeProbs: [String: Double]
}
class FlowerClassifier {
  convenience init()
  func prediction(flowerImage: CVPixelBuffer) throws -> FlowerClassifierOutput
}
```


### More Advanced  -  Underlying API


```swift
class FlowerClassifier {
  convenience init()
  let model: MLModel
  func prediction(flowerImage: CVPixelBuffer) throws -> FlowerClassifierOutput
}
```

Programmatic access to model for power users


### MLModel

```swift
class MLModel {
  var modelDescription: MLModelDescription
  func prediction(from input: MLFeatureProvider) throws -> MLFeatureProvider
}
```

Access to model description

Flexibility in how input is provided

### Behind the Scenes - Model compilation

Quick initialization

Optimized prediction


### Model Goals

Reduce size

Improve accuracy

Decrease prediction times
