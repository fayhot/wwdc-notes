## [Pathfinding](4-pathfinding.md) | 2050| p29

### Concepts

* Pathfinding operates on a navigation graph
* Graphs are collections of nodes
* Nodes are joined by connections
* Connections are directional
* Optimal path exists between any two connected nodes


### GKGraph

* Abstract graph base class
* Container of graph nodes
* Dynamic add / remove nodes
* Connect new nodes
* Find paths between nodes
* Two specializations
  * Grid graphs
  * Obstacle graphs



### Overview
* Find paths in navigation graphs
* Generate navigation graphs from
* Obstacles
* Grids
* SpriteKit scenes
- Dynamically modify graphs

### GKGridGraph

- Specialized for a 2D Grid
- Creates nodes on the grid
  - Cardinal connections
  - Optional diagonal connections
- Easy add/remove of grid nodes


### GKObstacleGraph

* Specialized for pathing around obstacles
  * Obstacles are arbitrary polygons
* Dynamically add/remove obstacles
* Dynamically connect nodes
* Buffer radius
  * “Safety zone” around obstacles
  * Game-dependent size

```
GKObstacleGraph
obstacles bufferRadius
[addObstacles:]
[removeObstacles:]
[connectNodeUsingObstacles:]
[lockConnectionFromNode:]
[unlockConnectionFromNode:]
```

### GKObstacleGraph example

```
/* Make an obstacle - a simple square */
vector_float2 points[] = {{400,400}, {500,400}, {500,500}, {400,500}};
GKPolygonObstacle *obstacle = [[GKPolygonObstacle alloc] initWithPoints:points count:4];

/* Make an obstacle graph */
GKObstacleGraph *graph = [GKObstacleGraph graphWithObstacles:@[obstacle] bufferRadius:10.0f];

/* Make nodes for hero position and destination */
GKGraphNode2D *startNode = [GKGraphNode2D nodeWithPoint:hero.position];
GKGraphNode2D *endNode = [GKGraphNode2D nodeWithPoint:goalPosition];

/* Connect start and end node to graph */
[graph connectNodeUsingObstacles:startNode];
[graph connectNodeUsingObstacles:endNode];

/* Find path from start to end */
NSArray *path = [graph findPathFromNode:startNode toNode:endNode];

```

### Advanced: GKGraphNode

* Graph node base class
* Subclass for
  * Advanced or non-spatial costs
  * Control over pathfinding
* Create your own graphs
  * Manually manage connections
  * Good for abstract or non-spatial graphs

### SpriteKit integration
Easily generate obstacles from SKNode bounds, physics bodies, or textures

```
/* Makes obstacles from sprite textures */
(NSArray*)obstaclesFromSpriteTextures:(NSArray*)sprites accuracy:(float)accuracy;
/* Makes obstacles from node bounds */
(NSArray*)obstaclesFromNodeBounds:(NSArray*)nodes;
/* Makes obstacles from node physics bodies */
(NSArray*)obstaclesFromNodePhysicsBodies:(NSArray*)nodes;
```


### Demo - SpriteKit integration | 2640
