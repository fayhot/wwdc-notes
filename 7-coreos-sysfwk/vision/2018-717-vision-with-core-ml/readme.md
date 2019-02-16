
# [2018 717 Vision with Core ML](https://developer.apple.com/videos/play/wwdc2018/717)

- Frank Doepke, Flat Pixel Enthusiast

Topic|Time|Page
---|---|---
• Custom Image classification
• Object recognition
• Vision fundamentals


### The Storyline

- Create an app helping shoppers identify items
  - Train a custom classifier
  - Build an iOS app
  - Keep an eye on pitfalls


### Our Training Regimen - Train using Create ML

- Take pictures
-  Sort into folders—the folder names are used as labels
  - How much data do I need
    - Minimum of 10 per category but more is better
    - Highly imbalanced datasets are hard to train
  - Augmentation adds some robustness on top of it but doesn’t replace variety


### Vision FeaturePrint.Scene

- Vision Frameworks FeaturePrint for Image Classification
  - Available through ImageClassifier training in Create ML
  - Trained on a very large dataset
  - Capable of predicting over 1000 categories
  - Powers user facing features in Photos
  - Continuous improvement
    - You might want to retrain in the future


