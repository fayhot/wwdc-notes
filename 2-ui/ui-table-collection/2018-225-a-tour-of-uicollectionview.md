# [2018 225 A Tour of UICollectionView](https://developer.apple.com/videos/play/wwdc2018/225)

- Steve Breen, UIKit Frameworks Engineer
- Mohammed Jisrawi, UIKit Frameworks Engineer

Agenda

• Build an app


- Layouts
- Updates
- Animations



### Key UICollectionView Concepts

- Layout
- Data source
- Delegate

UICollectionViewLayout

- Visual arrangement of content
- UICollectionViewLayoutAttributes
  - Bounds, center, and frame...
- Invalidation
- Animate between layouts

UICollectionViewFlowLayout

- Concrete subclass of UICollectionViewLayout 
- UICollectionViewDelegateFlowLayout extends UICollectionViewDelegate
- Line-based layout covers a wide range of designs



### UICollectionViewDataSource

- Provides content
- Section and item counts

optional func numberOfSections(in collectionView: UICollectionView) -> Int

func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int)
-> Int

func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell


UICollectionViewDelegate

- Optional
- Extends UIScrollViewDelegate
- Fine-grained control
  - Highlighting
  - Selection
- View appearance events
  - willDisplayItem
  - didEndDisplayingItem

x

## Demo - Getting started with UICollectionView


## When to Go Custom?

Can we use UICollectionViewFlowLayout?

Our fancy layout is not line-based

Start with flow before going custom!

### Creating a Custom UICollectionViewLayout

- Not complicated!
- Four basic methods
- ...and one additional method to consider...

### Providing Content Size

- open var collectionViewContentSize: CGSize { get }
- Size of bounds which contains all items
- Needed for UIScrollView.contentSize


### Providing Layout Attributes

- `func layoutAttributesForElements(in rect: CGRect) -> [UICollectionViewLayoutAttributes]?`
- `func layoutAttributesForItem(at indexPath: IndexPath) -> UICollectionViewLayoutAttributes?`
- Query by geometric region
- Query by IndexPath
- Performance matters

### Preparing the Layout

- func prepare()
- Called for every invalidateLayout
- Cache UICollectionViewLayoutAttributes
- Compute collectionViewContentSize

### Handling Bounds Changes in Your Custom Layout

- `func shouldInvalidateLayout(forBoundsChange newBounds: CGRect) -> Bool`
- Called for every bounds change
Size change Origin change
Called during scrolling 😳
Default implementation returns false



## Our Totally Cool Update Animation

- 1. Reload last item
- 2. Move last -> first
- 3. Delete 3rd item



### performBatchUpdates()

- `func performBatchUpdates(_ updates: (() -> Void)?, completion: ((Bool) -> Void)? = nil)`
- Animate updates together
- Perform data source updates and collection view updates in updates closure
- Collection view updates ordering does not matter...
- ...data source updates ordering does matter

### Collection View Updates Coalescing

Action |Notes| Index Path Semantics
---|---|---
Delete|Descending IndexPath order| Before updates
Insert|Ascending IndexPath order| After updates
Move||From: Before updates To: After updates
Reload|Decompose: Delete and inserts| Before updates


### Applying Data Source Updates

- Decompose Move into Delete and Insert updates
- Combine all Delete and Insert updates
- Process Delete updates first, in descending order
- Process Insert updates last, in ascending order


### What About reloadData()?

- No updates required
- Resync data source to collection view
- Not animated
- “The Sledgehammer”

•Demo
• Saving our totally cool update animation


Call to Action

- Build custom layouts
- Update animations
- DON'T Reload data

