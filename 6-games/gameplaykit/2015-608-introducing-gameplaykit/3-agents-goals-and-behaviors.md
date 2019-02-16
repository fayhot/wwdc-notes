## [Agents, Goals, and Behaviors](2015-608-3-agents-goals-and-behaviors.md) | 1230 | p19


### Concepts

* Agents are autonomously moving entities
* Driven by behaviors and goals Realistic constraints
* Behaviors are made up of goals
* Goals combined via weights

### Background

* Games need believable movements
* Organic behaviors look intelligent
* Realistic movement
* Has inertia
* Avoids obstacles Avoids other entities Follows paths


### GKAgent

* Simple autonomous point-mass
* Is a GKComponent
* Update applies behavior
* Goals change acceleration Velocity, position, rotation updated
* Units are dimensionless
* Game-world specific


### GKBehavior

* Dictionary-like container of goals
* Dynamically modify behavior
* Add/remove goals Modify weights
* Set behavior on agent to use it


### Example

```
/* Make some goals, we want to seek the enemy, avoid obstacles, target speed */
GKGoal *seek = [GKGoal goalToSeekAgent:enemyAgent];
GKGoal *avoid = [GKGoal goalToAvoidObstacles:obstacles];
GKGoal *targetSpeed = [GKGoal goalToReachTargetSpeed:50.0f];
/* Combine goals into behavior
GKBehavior *behavior = [GKBehavior behaviorWithGoals:@[seek,avoid,targetSpeed]
                                          andWeights:@[@1.0,@5.0,@0.5]];
/* Make an agent - add the behavior to it */
GKAgent2D *agent = [[GKAgent2D* alloc] init];
agent.behavior = behavior;
```

### GKAgentDelegate

* Sync graphics, animations, physics, etc.
* [agentWillUpdate:] called before updates
* [agentDidUpdate:] called after updates


### SpriteKit delegate example
```
@implementation MyAgentSpriteNode
...
- (void)agentWillUpdate:(GKAgent2D *)agent {
    /* Position the agent to match our sprite */
    agent.position = self.position;
    agent.rotation = self.zRotation;
}
- (void)agentDidUpdate:(GKAgent2D *)agent {
    /* Update the sprite’s position to match the agent */
    self.position = agent.position;
    self.zRotation = agent.rotation;
}
...
@end
```

### Demo - Agents and goals | 1740
