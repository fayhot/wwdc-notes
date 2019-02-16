## [Pathfinding](1-pathfinding.md) [2:00~]

### GKMeshGraph

### Custom node classes
Can attach custom data and logic to nodes
Generic support; no casting required



### // Mesh graph example

```swift
// Create mesh graph of space between (0,0) and (1000,1000)
let meshGraph = GKMeshGraph(bufferRadius:10.0,
                        minCoordinate:float2(0.0,0.0), maxCoordinate:float2(1000.0,1000.0))
// Set triangulation mode - Nodes at triangle vertices and centers
meshGraph.triangulationMode = [.vertices, .centers]

// Add obstacles and triangulate
meshGraph.addObstacles(obstacles)
meshGraph.triangulate()
```
