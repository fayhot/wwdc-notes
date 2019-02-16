
# [2017 710 Core ML in depth](https://developer.apple.com/videos/play/wwdc2017/710/)

* Krishna Sridhar, Core ML
* Zach Nation, Core ML



No|Topic|Presenter|Time|Page
--|--|--|--|--
1|Use cases|Krishna|240|p19
2|Hardware optimized|Krishna|1900|p72
3[Obtaining models](obtaining-models.md)|Zach|2115|p81


Development Flow

```swift
let model = FlowerClassifier()
if let prediction = try? model.prediction(image: image) { return prediction.flowerType
}
```

## This Session - TOC

## Use cases

* Sentiment Analysis
* Personalization
* Gesture Recognition
* Style Transfer
* Object Detection
* Music Tagging
* Summarization

### Models as Functions

Value Type | Data Type
--|--
Numeric | Double, Int64
Categories | String, Int64
Images | [CVPixelBuffer](https://developer.apple.com/documentation/corevideo/cvpixelbuffer-q2e)
Arrays |  [MLMultiArray](https://developer.apple.com/documentation/coreml/mlmultiarray)
Dictionaries | [String : Double], [Int64 : Double]


## Working with Text

Example | Input | Model
--|--|--
1 Sentiment Analysis | Word Counts | NN
2 Predictive Keyboard| Sequence of words |LSTM


### Using Other Formats

Word Counts

### Making Predictions


### Language Models


### Shakespeare Keyboard


## Hardware Optimized
