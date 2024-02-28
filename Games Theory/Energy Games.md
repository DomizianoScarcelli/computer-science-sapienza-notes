---
Exam:
  - Games on Graphs
---
An Energy Game (that also can represent a mean payoff game) is represented by a graph with nodes that belongs to each one of the players in the game. The edges between nodes are weighted, and they represent the that a player accumulates (positive weight) or looses (negative weight) when it passes trough it. Note that the player which the current node belongs to is the one that makes the move and the one that gains or looses energy.

An energy game solver has to find the minimum initial energy for each player in order for them to forever stay with a non-negative energy value, regardless their moves.

In order for this to be possible, and so for the game to be solvable, the graph must not have cycles which sum is negative, otherwise if the player goes around this cycle they will lose an infinite amount of energy.