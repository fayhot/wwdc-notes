


## [Game AI](2-game-ai.md), Michael Brennan [20:40~]

### Minmax strategist

### Monte Carlo strategist (New)
* Best-first search
* Random sampling of state space
  * Selects player move
  * Simulates out new games
  * Finds win / loss
  * Back-progagates win likelihood
* Convergent on optimal move

### Monte Carlo strategist
* Fast performance
* Works on large state spaces
* Only needs win/loss condition
* Approximately optimal

### Elements

[GKMonte​Carlo​Strategist](https://developer.apple.com/reference/gameplaykit/gkmontecarlostrategist)
* Budget , Exploration parameter, game model

### Code

```swift
let gameModel = GoGameModel()
let strategist =



```

### Custom strategists

protocol [GKStrategist](https://developer.apple.com/reference/gameplaykit/gkstrategist) (iOS 9.1)

### Decision making [24:40]

Many ways to model logic

### GKDecisionTree
