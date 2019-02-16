
# [2017 703 Introducing Core ML](https://developer.apple.com/videos/play/wwdc2017/703/)

* Gaurav Kapoor, Core ML
* Michael Siracusa, Core ML
* Lizi Ottens, Core ML


No|Topic|Presenter|Time|Page
--|--|--|--|--
1|Intro. ML Frameworks|Gaurav
2|Core ML: Overview, Model|Michael|1250|p46
3|[Development Flow](development-flow.md) - Demo Flower|Lizi|2030|p82
-|The End||3124


## Intro


* Real Time Image Recognition
* Text Prediction
* Entity Recognition
* Sentiment Analysis
* Handwriting Recognition
* Style Transfer
* Search Ranking Personalization
* Speaker Identification
* Machine Translation
* Face Detection
* Music Tagging
* Image Captioning
* Emotion Detection
* Text Summarization


Step/Phase|Data
--|--
Training| Offline -> Learning algorithm -> Model
Inference| Data -> Model -> {Label + confidence }


### Challenges (if you handwrite the inference code)

* Correctness
* Performance
* Energy Efficiency


## ML Frameworks

* Your app
* Vision | NLP
* Core ML
* Accelerate | MPS

### Run on Device

* User Privacy
* Data Cost
* Server Cost
* Always Available - offline









## Core ML - Michael - 1250

* Overview
* Model
* Development Flow

### Design Goals

All 4 platforms (OSes)

Focus on the experience you are trying to enable

* Simple
  * Unified inference API
  * Xcode integration
* Performant
  * Fine tuned inference engines
  * Built on Accelerate and Metal
* Compatible
  * Public model format
  * Support for popular training libraries


## Model - -

## Development Flow
