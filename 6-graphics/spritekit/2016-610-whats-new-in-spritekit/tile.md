## Tile Map


## Tile Maps [8:30]

### What are tile maps?

### Why use tile maps?

Great for lots of different games and art styles

Top-down PRGs / Slide-scrolling platformers / Isometric city builders / Hex-based board games

## Demo [11]

auto-mapping

Tile set.

## Class overview [23]

```swift

```



### Class


Class | Description | Example
--|--|--
[`SKTileMapNode`](https://developer.apple.com/documentation/spritekit/sktilemapnode)|SKTileMapNode is the tile map<br/>Derived from SKNode<br/>Contains all of the placed tiles<br/>Needs a tile set to be able to place tiles
[`SKTileSet`](https://developer.apple.com/documentation/spritekit/sktileset)|SKTileSet contains all placeable tile groups<br/>Also defines the type of tiles it contains|Grid<br/>Isometric<br/>Hexagonal
[`SKTileGroup`](https://developer.apple.com/documentation/spritekit/sktilegroup)|SKTileGroup contains a set of related tiles<br/>Has rules that govern tile placement|Grass<br/>Water<br/>Stone
[`SKTileGroupRule`](https://developer.apple.com/documentation/spritekit/sktilegrouprule)|SKTileGroupRule controls how to interact<br/>Contains tile variants
[`SKTileDefinition`](https://developer.apple.com/documentation/spritekit/sktiledefinition)| defines tile appearance<br/>Allows for animation<br/>Images can be flipped and/or rotated



### Code

### // Creating Tile Maps and Setting Tiles

```swift
// Get the tile set
guard let  tileSet = SKTileSet(named: ”MyTileSet”) else { return }

// Create a tile map
let tileSize = CGSize(width: 32.0, height: 32.0)
let tileMap =SKTileMapNode(tileSet: tileSet, columns: 16, rows: 16, tileSize: tileSize)

// Get a tile group from the tile set
let tileGroup = tileSet.tileGroups.first

// Set tile group for a specific tile
tileMap.setTileGroup(tileGroup, forColumn: 4, row: 7)

// Fill the entire map with a tile group
tileMap.fill(with: tileGroup)




 ```

### // Check user data in the tile under the player’s sprite

```swift
// Convert the player’s position into the tile map’s frame of reference
let position = tileMap.convert(playerSprite.position, from: playerSprite)

// Get the column and row of the tile that contains the position
let column = tileMap.tileColumnIndex(fromPosition: position)
let row = tileMap.tileRowIndex(fromPosition: position)

// Get the tile definition in the tile the player’s sprite is over
guard let definition = tileMap.tileDefinition(atColumn: column, row: row) else { return }


// Access custom user data on the tile definition
let customUserData = definition.userData?.value(forKey: “MyKey”)

```
