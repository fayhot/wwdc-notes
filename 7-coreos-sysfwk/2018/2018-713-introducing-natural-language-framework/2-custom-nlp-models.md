•Custom NLP Models
Doug Davidson, Senior Software Engineer


Concept Learning
 Classify Examples and
Understand


Machine Learning
 Training Data
Classify and Understand



Types of Custom Model

- Text Classification
- Word Tagging


Text Classification

x|x
--|--
Sentiment classification|
Topic classification|
Domain classification|


Word Tagging

x|x
--|--
Part of speech|
Named entity|
Slot parsing|
Chunking|



Supervised Machine Learning
Training and inference
Training

Custom NLP Models
Training



Text Classifier

```swift
import CreateML
import Foundation
let trainingData = try MLDataTable(contentsOfFile: Bundle.main.url(forResource: “news”, withExtension: “json”)!)
let model = try MLTextClassifier(trainingWith: trainingData,
textColumn: “text”, labelColumn: “label”)
try model.write(to: URL(fileURLWithPath: “/Users/me/Desktop/textclassifier.mlmodel”)

```

Word Tagger


Annotated Data

```swift
import CreateML
import Foundation
let trainingData = try MLDataTable(contentsOfFile:
Bundle.main.url(forResource: “products”, withExtension: “json”)!) let model = try MLWordTagger(trainingWith: trainingData,
tokenHeader: “tokens”, labelColumn: “labels”)
try model.write(to: URL(fileURLWithPath: “/Users/me/Desktop/wordtagger.mlmodel”)
```


Natural Language
Inference

Using a Custom Model


```swift
import NaturalLanguage
if let modelURL = Bundle.main.url(forResource: “classifier”, withExtension: “mlmodelc”) {
let model = try NLModel(contentsOf: modelURL)
let label = model.predictedLabel(for: “I really loved it!”)

```


Using Custom Models with NLTagger


