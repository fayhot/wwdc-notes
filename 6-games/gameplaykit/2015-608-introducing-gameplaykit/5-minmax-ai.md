
## [MinMax AI](5-minmax-ai.md) - Ross Dexter | 2815| p51


### Example

* Many games need equal AI opponents
  * Can play the entire game
  * Play by the same rules as human players
* Chess, Checkers, Tic-Tac-Toe, etc.

---

* MinMax AI
  * Looks at player moves
  * Builds decision tree
  * Maximizes potential gain
  *  Minimizes potential loss
* Tic-Tac-Toe example
 * Right branch optimal
 * Other branches lead to potential loss


### Features

* AI-controlled opponents
* Suggest move for human players
* Best suited for turn-based games
  * Any game with discrete moves
* Variable difficulty
  * Adjust look ahead
  * Select suboptimal moves

### Overview

* Players, Possible Moves, Scores
* Game Model
* MinMax
* Best Move

### GKGameModel protocol

* Abstract of the current game state
  * List of players
  * Currently active player
  * Player scores
  * Possible player moves
* Apply moves for players
  * Changes game state

---

* GKGameModelUpdate
  * Abstract of a game move
  * Used by MinMax to build decision tree
  * Apply to GKGameModel to change state
* GKGameModelPlayer
  * Abstract for a player of the game
  * Players make moves via GKGameModelUpdate

x


### GKMinmaxStrategist

* Operates on a GKGameModel
* maxLookAheadDepth is search depth
* [bestMoveForPlayer:] for optimal outcome
  * Ties can be broken at random
* [randomMoveForPlayer:] for N best moves
* Returns a GKGameModelUpdate

```
GKMinmaxStrategist
gameModel maxLookAheadDepth
[bestMoveForPlayer:]
[randomMoveForPlayer:]
```


### GKMinmaxStrategist example

```
/* ChessGameModel implements GKGameModel */
ChessGameModel *chessGameModel = [ChessGameModel new];
GKMinmaxStrategist *minmax = [GKMinmaxStrategist new];
minmax.gameModel = chessGameModel;
minmax.maxLookAheadDepth = 6;
/* Find the best move for the active player */
ChessGameUpdate *chessGameUpdate =
            [minmax bestMoveForPlayer:chessGameModel.activePlayer];
/* Apply update to the game model */
[chessGameModel applyGameModelUpdate:chessGameUpdate];
```

### Demo -  Stone Flipper AI
