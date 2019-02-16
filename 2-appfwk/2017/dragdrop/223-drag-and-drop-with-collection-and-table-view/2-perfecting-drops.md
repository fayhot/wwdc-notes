
## [Perfecting Drops](2-perfecting-drops.md) -- Tyler |  1120 | p34

### Drop Proposal

How you want to handle the drop

- UIDropProposal
  - UICollectionViewDropProposal
  - UITableViewDropProposal

operation: .copy .move .cancel .forbidden

#### Drop Intent

Additional information for collection and table view

- .unspecified
- .insertAtDestinationIndexPath
- .insertIntoDestinationIndexPath
- .automatic

```swift
// Providing a Drop Proposal
func collectionView(_ collectionView: UICollectionView, 
    dropSessionDidUpdate session: UIDropSession, 
    withDestinationIndexPath destinationIndexPath: IndexPath?) 
    -> UICollectionViewDropProposal {

    if session.localDragSession != nil {
        return UICollectionViewDropProposal(operation: .move,
            intent: .insertAtDestinationIndexPath)
    } else {
        return UICollectionViewDropProposal(operation: .copy, 
            intent: .insertAtDestinationIndexPath)
    } 
}
```

## Drop Animation []

Set up animations using the drop coordinator

```swift 
// Drop to a Newly Inserted Item
func collectionView(_ collectionView: UICollectionView, 
    performDropWith coordinator: UICollectionViewDropCoordinator) {

    guard let destinationIndexPath = coordinator.destinationIndexPath, 
        let dragItem = coordinator.items.first?.dragItem, 
        let image = dragItem.localObject as? UIImage
    else { return }

    collectionView.performBatchUpdates({    
        self.imagesArray.insert(image, at: destinationIndexPath.item) 
        collectionView.insertItems(at: [destinationIndexPath])
    })
    coordinator.drop(dragItem, toItemAt: destinationIndexPath) 
}
```

Drop into an item/row




```swift 
// Drop Into a Row

func tableView(_ tableView: UITableView, 
    performDropWith coordinator: UITableViewDropCoordinator) {

    guard let destinationIndexPath = coordinator.destinationIndexPath, 
        let dragItem = coordinator.items.first?.dragItem,
        let image = dragItem.localObject as? UIImage
    else { return }

    let photoAlbumIndex = destinationIndexPath.row

    guard photoAlbumIndex < self.albumsArray.count 
    else { return } 
    
    self.add(image: image, toAlbumAt: photoAlbumIndex)
    
    if let cell = tableView.cellForRow(at: destinationIndexPath),
        let view = cell.imageView {       
        
        let rect = cell.convert(view.bounds, from: view)
        coordinator.drop(dragItem, intoRowAt:    destinationIndexPath, rect: rect)
    } 
}
```

x

- Drop to an item/row
- Drop into an item/row
- Drop to a target
- Animate to any location with a transform


### Animating Items Before the Data Loads

- Data loads asynchronously
- Bookkeeping is difficult



## Introducing Placeholders (28)

- Temporary insertions in the collection/table view
- You provide the cell, we do the bookkeeping for you
- Great experience while data loads asynchronously

### Using the Placeholder Context

- Commit the insertion of a placeholder to exchange it for the final cell 
- Delete the placeholder if it’s no longer needed


### the Placeholder Context

```swift
// Using the Placeholder Context
for item in coordinator.items {
    let placeholderContext = /* insert the placeholder for this item */
    item.dragItem.itemProvider.loadObject(ofClass: UIImage.self) { (object, error) in 
        DispatchQueue.main.async {
            if let image = object as? UIImage {         
                placeholderContext.commitInsertion {    
                    insertionIndexPath in
                    self.imagesArray.insert(image, at: insertionIndexPath.item) 
                }
            } else { 
                placeholderContext.deletePlaceholder()
            }
        }
    } 
}
```

### Working with Placeholders

- Avoid reloadData , use performBatchUpdates(_:completion:) instead
- When placeholders exist, the table or collection view has uncommitted updates
- `var hasUncommittedUpdates: Bool { get }`


## Demo Placeholder
