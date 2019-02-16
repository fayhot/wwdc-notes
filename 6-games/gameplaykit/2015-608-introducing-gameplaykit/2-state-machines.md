
## [State Machines](2-state-machines.md) | 840 | p13

* Backbone of many gameplay elements
* Games are a collection of state machines
  * Animation, AI, UI, levels, etc.
* Common implementation removes boilerplate
* States reused throughout your game

IdleAnimation
MoveAnimation
AttackAnimation



### GKStateMachine

* General purpose finite state machine
  * Single current state
  * All possible states
* [enterState] causes state transition
  * Checks if transition is valid
  * Calls [exit] on previous,  [enter]on next state
* Updates currentState

### GKState

* Abstract class
* Implement logic in Enter/Exit/Update
  * These are called by the state machine
* Override [isValidNextState:]   to control edges
  * By default, all edges are valid
  * Can be dynamic, based on internal state

### Example

```
/* Make some states - Chase, Flee, Defeated, Respawn */
ChaseState *chase = [ChaseState state];
FleeState *flee = [FleeState state];
DefeatedState *defeated = [DefeatedState state];
RespawnState *respawn = [RespawnState state];
/* Create a state machine */
GKStateMachine *stateMachine = [GKStateMachine stateMachineWithStates:
                                                    @[chase, flee, defeated, respawn]];
/* Enter our initial state - Chase */
[stateMachine enterState:chase];
```
