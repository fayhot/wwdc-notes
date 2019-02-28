## [Smooth Scrolling](4-smooth-scrolling.md)|2740|p110

### Why Is My App Slow?

Dropping frames

- Computation
- Graphics (Compositing)


> 2016 Using Time Profiler in Instruments  


### Too Much Computation

- [`UICollectionView`](https://developer.apple.com/documentation/uikit/uicollectionview) and [`UITableView`](https://developer.apple.com/documentation/uikit/uitableview) prefetching
- Push more work to background queues


> [2016 219 What’s New in UICollectionView in iOS 10](https://developer.apple.com/videos/play/wwdc2016/219/) 

### Work to Push to the Background

- Network and file system access
- Image drawing
- Text sizing


> 2014 Advanced Graphics and Animations for iOS Apps 


### Complex Graphics

- Visual effects
- Masking

### Smooth Scrolling

- Run Time Profiler and Core Animation instruments on your app
- Keep work off the main thread
- Use visual effects and masking sparingly

> 2015 Profiling in Depth