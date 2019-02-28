## [Laser-Fast Launches](3-laser-fast-launches.md)|2030|p84

> [2017 413 App Startup Time: Past, Present, and Future](https://developer.apple.com/videos/play/wwdc2017/413)

> [2016 406 Optimizing App Startup Time](https://developer.apple.com/videos/play/wwdc2016/406)



Anatomy of a Launch


• Process Forking
• Dynamic Linking
• UI Construction
• First Frame
• Extended Launch Actions


### Dynamic Linking

- Allocating memory for execution
- Linking libraries and frameworks
- Initialization of Swift, Objective-C, Foundation, etc.
- Static object initialization
- 40–50 percent of typical app launch time


Avoid code duplication
Limit use of third-party libraries Avoid static initializers

> App Startup Time—Past, Present, and Future WWDC 2017

### UI Construction

- Prepare UI
- State restoration
- Load preferences
- Load model data




- Return quickly from
  - `application(_:willFinishLaunchingWithOptions:)`
  - `application(_:didFinishLaunchingWithOptions:)`
  - `applicationDidBecomeActive(_:)`
- Avoid writing to disk
- Avoid loading very large data sets
- Check database hygiene


### First Frame

- Core Animation renders your first frame
- Text drawing
- Image loading and decompression
- Only prepare the UI you need
- Avoid hiding views and layers

Extended Launch Actions

- Tasks deferred to post-launch
- App is responsive, but not yet usable
- Prioritize loading content that should be visible at launch
- Design for poor network conditions




### Always Be Measuring

- Use Time Profiler to measure your launch
- Measure regularly
- Use statistical averages

### Laser-Fast Launches

- Get responsive fast
- Use only what you need
- Measure, measure, measure