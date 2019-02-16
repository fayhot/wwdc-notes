
## Best Practices


Envisioning a Vision Task

* which image type is right for me?
* what am i going to do with the image?
* what performance do I need or want?

### Which Image Type Is Right for Me?

* Vision supports various image types
  * CGImage/CGImageRef
  * CIImage
  * CVPixelBuffer/CVPixelBufferRef
  * URL/NSURL
  * Data/NSData
* The image type to choose depends on where the image comes from
* You shouldn’t have to pre-scale the image
* Make sure to pass in the EXIF orientation of the image

### Everything streaming

* CVPixelBuffer
* Comes from a CMSampleBuffer in the VideoDataOut of a camera stream
* Also a good low-level format to provide image data in memory


### Files from Disk or Web

* URL for image files on disk
* NSData for images from the web
* Least amount of memory footprint
* Vision will do the scaling without reading the full image if possible
* EXIF Orientation is derived from the file if possible but can be overwritten

### Core Image

* Already using Core Image
* Preprocessing the image


### Images Already Used in the UI

* Use CGImage if the image was already used in the UI
* UIImage and NSImage have accessors for CGImageRefs


### What Am I Going to Do with the Image?

* Interactively explore the image
  * Use VNImageRequestHandler and hold onto it
  * Remember that the input image is immutable
* Tracking an observation
  * Use VNSequenceRequestHandler
  * Tracking state is kept in the VNSequenceRequestHandler
  * Lifecycle of images is not tied to the life of the VNSequenceRequestHandler

### What Performance Do I Need or Want?

* Vision tasks can be time consuming and processing intensive
  * Dispatch your work on a queue with appropriate QOS
  * Use the completion handler to work with the results
  * Completion handler is called on the same queue as the request

### Yet Another Face Detector?

* Vision uses deep learning for face detection
  * Highest precision and recall
  * Slower on older hardware in particular

### Face Detector Landscape

X | Vision | Core Image | AV Capture
--|--|--|--
Accuracy|Best|Better|Good
Processing time|Fast|Faster|Fastest
Power usage|Good|Better|Best
Availability|iOS, macOS, tvOS|iOS, macOS, tvOS|iOS only

### CIDetector vs. Vision

* CIDetector will remain as they are in Core Image
* New algorithms will be exposed through Vision
* Algorithm improvements will be made available in Vision
