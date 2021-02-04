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


### Trie: insert(word), search(word) -> bool, start_with(prefix) -> bool

+ https://leetcode.com/problems/implement-trie-prefix-tree/
    * https://leetcode.com/problems/design-add-and-search-words-data-structure/
    * https://leetcode.com/problems/word-search-ii/
+ https://medium.com/@info.gildacademy/a-simpler-way-to-implement-trie-data-structure-in-python-efa6a958a4f2
+ https://towardsdatascience.com/implementing-a-trie-data-structure-in-python-in-less-than-100-lines-of-code-a877ea23c1a1
+ We can realize this by a dictionary of key: character, value: a tuple
  / namedtuple(children, end), children is another dictionary

```python
class Trie:

    def __init__(self):
        """
        Initialize your data structure here.
        - [children, end] = [dict(), False/True]
        """
        self.trie = [dict(), False]


    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        cur = self.trie
        for c in word:
            # resulting value = get child 'c' in children, if not exist return [dict(), False]
            # bind cur[0][c] to the resulting value
            # then bind cur to the resulting value
            cur[0][c] = cur = cur[0].get(c, [dict(), False])

            ## simpler to understand version
            # if c not in cur[0]:
            #     cur[0][c] = [dict(), False]
            # cur = cur[0][c]
        cur[1] = True   # set the end of the word

    def _dfs(self, word):
        cur = self.trie
        for c in word:
            if c not in cur[0]: return None
            else: cur = cur[0][c]
        return cur


    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        node = self._dfs(word)
        if node is None: return False
        else: return node[1]



    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        node = self._dfs(prefix)
        return node is not None


# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```

## Cycles

## Shortest Paths

## Maximum Flow

## Connectivity

## Topological Sort

- https://en.wikipedia.org/wiki/Topological_sorting
    + A directed acyclic graph (DAG) has a topological order.
- Kahn's algorithm:
    + Find a node without any incoming edges (break tie
      lexicographically or arbitrarily)
    + Add the node to the end of the sorted list
    + Remove the node and all of its outgoing edges
    + Repeat
- Depth-first search
    + Depth-first search until find a node that has no outgoing edges
    + Add the node to the start of the sorted list
    + Mark the node is visited


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
