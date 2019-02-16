
# [2018 712 A Guide to Turi Create](https://developer.apple.com/videos/play/wwdc2018/712)

2018-712-a-guide-to-turi-create


## What is Turi Create?

- Python library for creating Core ML models
- Easy to use, no need to be an ML expert
- Task focused APIs
- Cross platform (Mac, Linux)
- Open source

Join the community https://github.com/apple/turicreate

5 steps 

https://github.com/apple/turicreate


## 5 step recipe for creating   Core ML models

Step|What to do
---|---
Task|What are you trying to do?
Data|What data do you need?
Model|Create   a model
Evaluate|Is the model any good?
Deploy|Add Core ML model to your app



## Code 

```python 
import turicreate
// Load data
data = turicreate.SFrame(“data.sframe”)
train, test = data.random_split(0.8)
// Create a model
model = turicreate.object_detector.create(train, “labels”)
// Evaluate the model
metrics = model.evaluate(test)
// Export for deployment
model.export_coreml(“MyModel.mlmodel”)
```

## What is an SFrame 


```
[ 
    {
    "label" : "coffee", 
    "coordinates" : {
        "x"      : 387,
        "y"      : 660,
        "height" : 550,
        "width"  : 814,
    }
    }, {
    "label" : "croissant", 
    "coordinates" : {
        "x"      : 800,
        "y"      : 630,
        "height" : 373,
        "width"  : 812,
    }
} ]
```

Disk backed, tabular data structure
Common data manipulation tasks
Work with   text, images, and json
Interactively explore and visualize data


## Demo • Calorie counting 

## Demo Recap

- Loaded images and annotations into the SFrame
- Interactively explored data
- Created a model
- Evaluated quantitatively
- Exported to Core ML


•Exciting New features in 5.0


## Turi Create 5.0

- New Task
  - Style Transfer
- Performance
  - Native GPU Acceleration on Macs
- New Deployments
  - Recommenders
  - Vision Feature Print powered models

### Style Transfer  2400

```python 
import turicreate

// Load data
content_images = turicreate.load_images(“content/”)
style_images = turicreate.load_images(“style/”)

// Create a model
model = turicreate.style_transfer.create(content_images, style_images)

// Make predictions
stylized_images = model.stylize(content_images)
// Export for deployment
model.export_coreml(“MyStyles.mlmodel”)
```


## Demo   •Demo • Stylish filter creation app | | 

Demo Recap

- Loaded images into the SFrame
- Created a model
- Stylized images
- Visualized predictions
- Exported to Core ML

## Personalization

- Task: Recommend items for users
- Data: Historical preferences
- Deployment:
  - Core ML custom models
  - macOS 10.14, iOS 12
- Top community feature request




```swift 
let model = MyRecommender()
// Historical interactions
let input = [“BrownBeard”: 1.0,
        “BlackHandleBar”: 1.0,
        “BrownLongHair”: 1.0]

// Make predictions
let output = try model.prediction(interactions: input, k: 10)
// Consume predictions
let predictions = output.recommendations
let confidence = output.probabilities
```




## Recap: Create Core ML models for your intelligent apps

5 steps 


```python 
import turicreate
// Load data
data = turicreate.SFrame(“data.sframe”)
train, test = data.random_split(0.8)
// Create a model
model = turicreate.object_detector.create(train, “annotations”)

// Evaluate the model
metrics = model.evaluate(test)
// Export for deployment
model.export_coreml(“MyModel.mlmodel”)

```

