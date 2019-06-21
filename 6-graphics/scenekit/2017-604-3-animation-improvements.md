## [Animation Enhancement](2017-604-3-animation-improvements.md) |Amaury Balliet | 3400-3650 | p121

[API](https://developer.apple.com/documentation/scenekit/animation)



class [`SCNAnimation`](https://developer.apple.com/documentation/scenekit/scnanimation) : NSObject

class [`SCNAnimationPlayer`](https://developer.apple.com/documentation/scenekit/scnanimationplayer) : NSObject

protocol [`SCNAnimationProtocol`](https://developer.apple.com/documentation/scenekit/scnanimationprotocol)


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

Step, Walk, Run

### Performance


- Starting, pausing and stopping animations is much faster
- Efficient evaluation of skeletal animation


