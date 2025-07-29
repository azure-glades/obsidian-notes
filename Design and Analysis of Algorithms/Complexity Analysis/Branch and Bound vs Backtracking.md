[[Branch and Bound Approach]]
[[Backtracking Algorithms]]

| Backtracking           | Branch and Bound       |
| ---------------------- | ---------------------- |
| State space tree used  | State space tree used  |
| All possible solutions | Optimal Solution       |
| DFS Traversal          | DFS  and BFS Traversal |
| No bounding function   | Bounding function used |


AI Answer:

|**Feature**|**Backtracking**|**Branch-and-Bound**|
|---|---|---|
|**Primary Purpose**|Solves constraint satisfaction problems (finding _any_ valid solution)[4](https://en.wikipedia.org/wiki/Backtracking)[1](https://www.tutorialspoint.com/difference-between-backtracking-and-branch-n-bound-technique)[2](https://codecrucks.com/backtracking-vs-branch-and-bound/)|Solves optimization problems (finding the _best_ solution)[9](https://en.wikipedia.org/wiki/Branch_and_bound)[3](https://stackoverflow.com/questions/30025421/difference-between-backtracking-and-branch-and-bound)[2](https://codecrucks.com/backtracking-vs-branch-and-bound/)|
|**Search Strategy**|Depth-First Search (DFS)[4](https://en.wikipedia.org/wiki/Backtracking)[1](https://www.tutorialspoint.com/difference-between-backtracking-and-branch-n-bound-technique)[3](https://stackoverflow.com/questions/30025421/difference-between-backtracking-and-branch-and-bound)|Flexible: Best-First Search or Breadth-First Search with priority queues[5](https://id.scribd.com/doc/125863164/What-is-Difference-Between-Backtracking-and-Branch-and-Bound-Method)[7](https://blog.heycoach.in/backtracking-and-branch-and-bound/)[6](https://thisvsthat.io/backtracking-vs-branch-and-bound)|
|**Pruning Criteria**|Abandons partial solutions violating constraints[4](https://en.wikipedia.org/wiki/Backtracking)[1](https://www.tutorialspoint.com/difference-between-backtracking-and-branch-n-bound-technique)|Eliminates branches using cost bounds (cannot improve current best solution)[9](https://en.wikipedia.org/wiki/Branch_and_bound)[7](https://blog.heycoach.in/backtracking-and-branch-and-bound/)|
|**Solution Guarantee**|Finds all valid solutions[4](https://en.wikipedia.org/wiki/Backtracking)[2](https://codecrucks.com/backtracking-vs-branch-and-bound/)|Guarantees optimal solution[9](https://en.wikipedia.org/wiki/Branch_and_bound)[7](https://blog.heycoach.in/backtracking-and-branch-and-bound/)[6](https://thisvsthat.io/backtracking-vs-branch-and-bound)|
|**Memory Usage**|Generally lower (DFS-based)[6](https://thisvsthat.io/backtracking-vs-branch-and-bound)|Higher (maintains priority queue of nodes)[6](https://thisvsthat.io/backtracking-vs-branch-and-bound)|
|**Termination Condition**|Stops after finding first/all valid solutions[1](https://www.tutorialspoint.com/difference-between-backtracking-and-branch-n-bound-technique)[2](https://codecrucks.com/backtracking-vs-branch-and-bound/)|Explores entire search space to confirm optimality[9](https://en.wikipedia.org/wiki/Branch_and_bound)[2](https://codecrucks.com/backtracking-vs-branch-and-bound/)|
