
# [713 What's New in Location Technologies](https://developer.apple.com/videos/play/wwdc2017/713/)



* API improvements
* Authorization and usage reporting
* Best practices

## API improvements

### CLGeocoder Improvements

* Updated to support Contacts framework
  * Geocode CNPostalAddress
  * Obtain a CNPostalAddress from a CLPlacemark  
  * Address dictionary methods are deprecated
* Supports geocoding with a locale
  * Overrides user preference

### Heading vs. Course

* Better heading estimates
* Fully automatic
* Use CMDeviceMotion for raw heading

### Indoor Positioning Improvements

* Accuracy
* Responsiveness
* Availability
* Interoperability

### Continuous Background Location
Now available on watchOS

* Continuous location extends to background
* Previously available through HealthKit
* Good for navigation and fitness apps
* Workout apps must adopt
* Three easy steps
  * Background Modes
  *  locationManager.allowsBackgroundLocationUpdates = true
  * locationManager.startUpdatingLocation() // While in the foreground!!


### Best Practices for Workout Apps

Use HKWorkoutSession
Use CMPedometer for pedestrian distance

## Authorization and Usage Reporting
