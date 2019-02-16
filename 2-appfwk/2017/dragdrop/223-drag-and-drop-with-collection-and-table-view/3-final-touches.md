

## [Final touches](3-final-touches.md) -- Tyler|3030| p93


### Reordering



Supporting Reordering

Implement dropDelegate method

func collectionView(_: UICollectionView,  dropSessionDidUpdate: UIDropSession, 
withDestinationIndexPath: IndexPath?) -> UICollectionViewDropProposal

Return a drop proposal

return UICollectionViewDropProposal(operation: .move, intent: .insertAtDestinationIndexPath)

Reordering

Table View

Continue to implement the existing data source method
func tableView(_: UITableView, moveRowAt: IndexPath, to: IndexPath)

Called instead of tableView(_: UITableView, performDropWith: UITableViewDropCoordinator)

Reordering

Collection View

Provide a dragDelegate and dropDelegate

Inside collectionView(_: UICollectionView, performDropWith: UICollectionViewDropCoordinator)

- Delete from UICollectionViewDropItem.sourceIndexPath
- Insert at UICollectionViewDropCoordinator.destinationIndexPath


### Collection View Reordering Cadence

var reorderingCadence: UICollectionViewReorderingCadence { get set }
 
- .immediate
- .fast
- .slow

### Spring loading


Table and collection view conform to 

`UISpringLoadedInteractionSupporting var isSpringLoaded: Bool { get set }`

- Customize spring loading with the optional delegate method

`func collectionView(_: UICollectionView,  shouldSpringLoadItemAt: IndexPath, with: UISpringLoadedInteractionContext) -> Bool`

## Customizing Cell Appearance

.none .lifting .dragging

### Customizing the Drag Preview

