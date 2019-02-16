## [Animation Enhancement](2017-604-3-animation-improvements.md) |Amaury Balliet | 3400 | p121

[API](https://developer.apple.com/documentation/scenekit/animation)



SCNAnimation

SCNAnimationPlayer



- Introducing SCNAnimation and SCNAnimationPlayer
- Mutability while playing
  - Speed
  - Pausing
  - Blending
- Bridged with Core Animation
- Available on all platforms



### Old approach


```swift
// start walking
character.addAnimation(animation, forKey: "walk")

// later: stop walking, start jumping
character.removeAnimation(forKey: "walk")
character.addAnimation(jumpAnimation, forKey: "jump")
```


### New approach

```swift
// configure the players
character.addAnimationPlayer(walkAnimationPlayer, forKey: "walk") 
character.addAnimationPlayer(jumpAnimationPlayer, forKey: "jump")
 
 
// start walking
walkAnimationPlayer.play()
 
// later: stop walking, start jumping
walkAnimationPlayer.stop()
jumpAnimationPlayer.play()


// at any time: mutate the players
walkAnimationPlayer.speed = characterSpeed // walk slower or faster
runAnimationPlayer.blendFactor = walkRunFactor
// `walkRunFactor` of walk  `1.0 - walkRunFactor` of run

```


### Animation blending


### Performance


- Starting, pausing and stopping animations is much faster
- Efficient evaluation of skeletal animation


