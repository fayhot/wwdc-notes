
# [2017 605 SceneKit in Swift Playgrounds](https://developer.apple.com/videos/play/wwdc2017/605/)


## Prototyping

## Iterating  6

### 2.1 modelling the world - separate data and visuals

### 2.2 animation

SCNTransaction



### 2.3 add visual interests  13+

SCNReferneceNode

Moving the water - shader

### 2.4 accessibility support 16+

VoiceOver


## Tuning - s - 1940


```swift
view.showsStatistics = true
```

number of drawcall - diamond


### Reduce Draw Call Count

2 distict phases

* Geometry
* Materials
* Lighting

### Geometry

mesh on grass

if they do not move, draw one big mesh.  

1 draw call per mesh

Flattening Geometry

```swift
node.fattenedClone()
```

### Materials 2945


Reducing Materials

texture atlas

1 material = 70 original materials

### Lighting 3300
