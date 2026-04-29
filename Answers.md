# Pacman Search Project - Answers

## Question 1: Depth First Search (DFS)

I implemented graph-search DFS using a `Stack` from `util.py`. Each fringe item stores `(state, actions_list)`. A `visited` set prevents re-expanding states. When a state is popped, it's checked against the goal; if not the goal, its unvisited successors are pushed onto the stack with updated action lists. The exploration order goes deep before broad, so Pacman doesn't necessarily follow the most direct path—DFS doesn't guarantee least-cost solutions.

## Question 2: Breadth First Search (BFS)

BFS uses a `Queue` (FIFO) instead of a Stack. The key difference from DFS is that states are marked as visited when they are *enqueued* (not when popped), which prevents duplicate entries in the fringe and ensures the first path found to any state is the shortest in terms of number of actions. This guarantees an optimal solution when all step costs are equal.

## Question 3: Uniform Cost Search (UCS)

UCS uses a `PriorityQueue` where the priority is the cumulative path cost `g(n)`. Each fringe entry stores `(state, actions, cost)`. States are marked visited upon expansion (popping), not upon enqueueing, because a cheaper path to the same state might be discovered later. This correctly handles the `StayEastSearchAgent` and `StayWestSearchAgent` cost functions, producing low and high path costs respectively.

## Question 4: A* Search

A* extends UCS by adding a heuristic estimate `h(n)` to the path cost, using priority `f(n) = g(n) + h(n)`. The structure is identical to UCS except for the priority calculation. With `nullHeuristic` (h=0), A* behaves exactly like UCS. With `manhattanHeuristic`, A* expands fewer nodes than UCS on `bigMaze` (~549 vs ~620) while still finding the optimal solution.

## Question 5: Corners Problem

The state representation is a tuple `(position, visitedCorners)` where `position` is an `(x, y)` coordinate and `visitedCorners` is a tuple of corner coordinates that have been reached. The goal test checks if all four corners are in the visited set. In `getSuccessors`, when Pacman moves to a new position, the visited corners tuple is updated if the new position is one of the four corners. This compact representation avoids encoding irrelevant game state.

## Question 6: Corners Problem Heuristic

I used a greedy nearest-neighbor heuristic over Manhattan distances. Starting from the current position, the heuristic repeatedly selects the nearest unvisited corner (by Manhattan distance), adds that distance to a running total, and moves to that corner. This is admissible because each segment uses Manhattan distance (a lower bound on true path distance), and the greedy tour length lower-bounds the true optimal tour cost. It expanded 901 nodes on `mediumCorners`, well under the 1200 threshold for full credit.

## Question 7: Food Search Heuristic

The heuristic returns the maximum *maze distance* from Pacman's current position to any remaining food dot. Maze distance (computed via BFS) accounts for walls and gives the true shortest path to each food dot. Since Pacman must eventually reach every food dot, the farthest one provides a tight lower bound. Results are cached in `problem.heuristicInfo` to avoid recomputation. This expanded 4137 nodes on `trickySearch`, earning the extra credit point (under 7000 threshold).

## Question 8: Suboptimal Search (Closest Dot)

`findPathToClosestDot` simply calls `search.bfs(problem)` on an `AnyFoodSearchProblem`. The `AnyFoodSearchProblem.isGoalState` checks whether the current position contains food (`self.food[x][y]`). BFS finds the shortest path to the nearest food dot. This greedy approach is suboptimal overall—for example, if two food dots are near each other but far from Pacman, going to one then the other is shorter than always chasing the closest dot from the current position.
