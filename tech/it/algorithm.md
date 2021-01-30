[TOC]

# Overview

An algorithm is a self-contained step-by-step set of operations to be
performed.

# Dynamic Programming

- It is a mathematical optimization method and a computer programming
  method.
    + It was developed by Richard Bellman in the 1950s.
    + It refers to simplifying complicated problems by breaking it down
      into simpler sub-problems in a recursive manner.
- Two key attributes that a problem must have in order for dynamic
  programming to be applicable:
    + **optimal substructure**: means that the solution to a given
      optimization problem can be obtained by the combination of optimal
      solutions to its sub-problems
    + **overlapping sub problems**: means that the space of sub-problems
      must be small, that is, any recursive algorithm solving the
      problem should solve the same sub-problems over and over, rather
      than generating new sub-problems
- Dynamic programming solves each sub-problem only once by using two
  approaches
    + **Top-down**: memoize or store the solutions to the sub-problems in a
      table. Whenever we attempt to solve a new sub-problem, we first
      check the table to see if it is already solved. If a solution has
      been recorded, we can use it directly, otherwise we solve the
      sub-problem and add its solution to the table.
    + **Bottom-up**: try solving the sub-problems first and use their
      solutions to build-on and arrive at solutions to bigger
      sub-problems. This is also usually done in a tabular form by
      iteratively generating solutions to bigger and bigger sub-problems
      by using the solutions to small sub-problems.
- Introduction to DP: https://en.wikipedia.org/wiki/Dynamic_programming
- Quick review with some sample problems: http://www.csc.kth.se/~karlan/AoK/F6_15.pdf

# Graph

## Depth-first Search (DFS)

## Breath-first Search (BFS)

## Trees

- Binary Tree
    + Binary Search Tree (BST)
- Minimum Spanning Tree (MST)
- Disjoint-set data structures (multiway trees - unbounded number of
  branches per node)

## Cycles

## Shortest Paths

## Maximum Flow

## Connectivity

## Topological Sort

## Back Tracking


# String



## Others

- `A*` search algorithm
- Alpha-beta pruning
- Graph coloring
- Traveling Salesman Problem (TSP)

# Common examples

## Binary search

- Worst-case time complexity: O(logn)
- Average-case time complexity: O(logn)
- Worst-case space complexity: O(1)

```python
def bin_search(list, target) -> bool:
    lo, hi = 0, len(list) - 1
    while lo <= hi:
        mid = (lo + hi) // 2 # floor((lo+hi)/2)
        if list[mid] < target: lo = mid + 1
        elif list[mid] > target: hi = mid - 1
        else: return True
    return False
```

## Tic-tac-toe

Players choose the first available move from the following list:
1. **Win**: If the player has two in a row, they can place a third to
   get three in a row.
2. **Block**: If the opponent has two in a row, the player must play the
   third themselves to block the opponent.
3. **Fork**: Create an opportunity where the player has two threats to
   win (two non-blocked lines of 2).
4. **Blocking an opponent's fork**:
    - **Option 1**: The player should create two in a row to force the
      opponent into defending, as long as it doesn't result in them
      creating a fork. For example, if "X" has a corner, "O" has the
      center, and "X" has the opposite corner as well, "O" must not play
      a corner in order to win. (Playing a corner in this scenario
      creates a fork for "X" to win.)
    - **Option 2**: If there is a configuration where the opponent can
      fork, the player should block that fork.
5. **Center**: A player marks the center. (If it is the first move of
   the game, playing on a corner gives "O" more opportunities to make a
   mistake and may therefore be the better choice; however, it makes no
   difference between perfect players.)
6. **Opposite corner**: If the opponent is in the corner, the player
   plays the opposite corner.
7. **Empty corner**: The player plays in a corner square.
8. **Empty side**: The player plays in a middle square on any of the 4
   sides.

# References

[algo-visualizer]: https://github.com/parkjs814/AlgorithmVisualizer "Algorithm Visualizer"
[algo]: https://en.wikipedia.org/wiki/Algorithm "Wikipedia - Algorithm"
