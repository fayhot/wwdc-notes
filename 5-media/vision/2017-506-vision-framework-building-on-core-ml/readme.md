# [2017 506 Vision Framework: Building on Core ML](https://developer.apple.com/videos/play/wwdc2017/506/)


* Brett Keating, Apple Manager
* Frank Doepke, He who wires things together


No | Topic | Presenter | Time|Page
--|--|--|--|--
1|What Can Vision Do|
2|Vision Concepts| Frank Doepke | 815
3|[The Code](the-code.md)|1110|p43
4|[Best Practices](best-practice.md)|1230|p53
5|Demo: Show And Tell||1930|p77
6|Demo: Machine Learning | 2200
7|Show and Tell - Part Two / MNISTVision | 2510

## What Can Vision Do

* Face Landmarks, smaller face, strong profile,
  * Face Landmarks
* Image Registration
* Rectangle Detection
* Barcode Detection
* Text Detection
* Object Tracking
  * For faces, rectangles, and general templates
* Integration with Core ML

### On Devices vs. Cloud


## Vision Concepts - Frank - 815


concept | class | Analyzing an Image| Tracking in a Sequence
--|--|--|--
The Asks | Request| DetectBarcodes<br/>DetectFaceLandmarks<br/>DetectFaceRectangles|TrackObject<br/>TrackRectangle<br/>ImageRegistration
The Machinery | Handler|VNImageRequestHandler |VNSequenceRequestHandler
The Results | Observation|



### Image Request Handler

* For interactive exploration of an image
* Holds on to the image for its lifecycle
* Allows optimization of various requests performed on an image

### Sequence Request Handler

* For anything that looks at images in a sequence like tracking
* Does not optimize for multiple requests on an image

## [Putting It into Code](the-code.md)

## [Best Practices](best-practice.md)


## Show and Tell - Part One - 1930

AVCapture + Rectangle.

## Machine Learning - 2200

## Show and Tell - Part Two - 2510


### MNISTVision 2510

Concepts to be covered
* Spin off requests from other requests
* Use Core Image for processing
* Use Core ML for machine learning

### The Flow Chart

Step|What to do
--|--
1|Find sticky note using Rectangle Detector
2|Use CI for perspective correction and image processing
3|Run MNIST classifier on resulting CIImage



## Show and Tell - Part Two - 2510
