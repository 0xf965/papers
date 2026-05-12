# Snake Game – Game Guide (Game of Prompts)

## Description

This game is an automated version of Snake.
The player does not directly control the snake; instead, they create a solver that decides each move based on the current game state.

The goal is to achieve the highest possible score.



## Objective

* Eating normal apples gives +1 point
* Eating poisonous apples subtracts -2 points (minimum 0)
* The game ends if the snake:

  * Collides with the borders
  * Collides with itself
  * Receives an invalid move or does not respond



## How the game works

The game progresses in steps. In each step, the following happens:

1. The Game Service sends the current state
2. The solver decides a move
3. The Game Service applies that move
4. The state and score are updated
5. The process repeats



## What information the solver receives

At each step, the solver receives:

* Full position of the snake (the head is the first element)
* Position of the apple
* Positions of poisonous apples
* Board size

Example concept:

```
snake = [[10,10], [10,9], [10,8]]
apple = [12,15]
poison_apples = [[11,15]]
board_rows = 60
board_cols = 120
```



## What the solver must return

The solver must return exactly one move:

```
UP
DOWN
LEFT
RIGHT
```

Only one per turn.



## Simple example

State:

* Head at (10,10)
* Apple at (10,15)

Interpretation:

* RIGHT moves closer to the apple
* LEFT may be invalid if there is body
* UP or DOWN may move away

The solver must choose the most appropriate move in that context.



## Scoring

* Normal apple: +1
* Poisonous apple: -2 (minimum 0)

Number of poisonous apples on the board:

```
poison_apples = floor(score / 10)
```

Higher score increases difficulty.



## Solver constraints

* The solver runs in isolation
* It cannot connect to the internet or external services
* The full solver image (including dependencies) must not exceed 1 GB



## What makes a good solver

A good solver does not only chase the apple. It must also:

* Avoid collisions at all times
* Avoid decisions that leave it without escape options
* Handle tight spaces correctly
* Avoid poison when necessary
* Be consistent and never fail or return invalid moves

In many cases, going directly toward the apple is not the best decision.



## Reproducibility

The game can be run with a seed:

same solver + same seed = same result

This allows fair comparison between solvers.



## Summary

The problem the solver must solve is:

Given a game state, decide the best possible move at that moment.

This process repeats continuously until the game ends.
