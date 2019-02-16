
# [2012 219 Advanced Collection Views and Building Custom Layouts](https://developer.apple.com/videos/play/wwdc2012/219/)


2012-219-advanced-collection-views-and-building-custom-layouts.md



* Deeper architectural understanding
* Go far with UICollectionViewFlowLayout
* Build your own layout



## Concepts and Architecture



Decoration views are layout driven



UICollectionViewLayoutAttributes



UICollectionViewDelegateFlowLayout : UICollectionViewDelegate : UIScrollViewDelegate



Change == layout invalidation

Implicit invalidations with performBatchUpdates: completion:

## [14] Advanced [`UICollectionViewFlowLayout`](https://developer.apple.com/documentation/uikit/uicollectionviewflowlayout)


* Add new kinds of view
* Tweak layout attributes
* Add new layout attributes
* Add gesture support
* Customize insert and delete animations

## [20:30 - 25:20] Demo: Pinch resizing gesture ( in FlowLayout) - Mathieu Martin



## [25:45] Writing Custom Layouts



Required overrides

- collectionViewContentSize

- layoutAttributesForElementsInRect:



- layoutAttributesForItemAtIndexPath:

- layoutAttributesFor
