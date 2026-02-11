Finding solutions by searching the set of possible solutions (searching the state space)
> See further [[Adversarial Search]] 

Used by goal-based agents to identify strategies. Only possible when there is a search space - a set of states that can be visited logically, allowing us to precompute the sequence that leads to best outcome

1. **uninformed search:** when there is no way to know how close we are to a goal. *blind search* - since one cannot evaluate which node is better without actually visiting it. Only 2 things are known. No information about how far away we are from the goal
	- Know how to reach next states from current state
	- Know whether current state is a valid solution or not.
	Ex: BFS, DFS, Depth-limited search, iterative deepening dfs
2. **informed search:** when we can guess/estimate/know exactly how close we are to a goal. domain knowledge is present to guide the search more effectively. called *heuristic search*
	Ex: A\* search, best first search

# Uninformed Search
These algorithms explore the state space without any prior knowledge about the distance to the goal.

## Breadth-First Search (BFS)
- **Thinking Process:** Explore the graph layer by layer. Find the shallowest goal first.
- **Key Idea:** Use a **FIFO Queue**. Expand all nodes at depth $d$ before moving to $d+1$.
	- **Simple Algorithm:**
    1. Place the starting node in a Queue.
    2. While the queue is not empty:
        - Remove the first node.
        - If it's the goal, stop.
        - Otherwise, add all unvisited neighbors to the **back** of the queue
    
    > Completeness: Guaranteed to find a solution if one exists (on finite graphs).
    > Optimality: Only optimal if all step costs are equal.

## Depth-First Search (DFS)
- **Thinking Process:** Go as deep as possible down one path before backtracking.
- **Key Idea:** Use a **LIFO Stack** (or recursion).
- **Simple Algorithm:**
    1. Place the starting node in a Stack.
    2. While the stack is not empty:
        - Pop the top node.
        - If it's the goal, stop.
        - Otherwise, push all unvisited neighbors onto the stack.
    > Space Complexity: Much more efficient than BFS ($O(bm)$ vs $O(b^d)$).
    > Optimality: Not optimal; it may find a very "deep" solution while a shallow one exists.

## Depth-limited Search

## Iterative Deepening Depth-First Search

## Uniform-Cost Search (UCS)
- **Thinking Process:** Always expand the "cheapest" node seen so far.
- **Key Idea:** Use a **Priority Queue** ordered by path cost $g(n)$.
- **Simple Algorithm:**
    1. Place start node in Priority Queue with priority 0.
    2. While queue is not empty:
        - Pop node $n$ with the lowest $g(n)$.
        - If $n$ is the goal, stop (this ensures the cheapest path).
        - For each neighbor, calculate $g(neighbor) = g(n) + \text{step cost}$.
    > Optimality: Optimal for any non-negative step costs.
    > Relation: BFS is just UCS where all step costs are equal to 1.



# Informed (Heuristic) Search
These algorithms use a heuristic function $h(n)$ to estimate the cost from node $n$ to the goal.
> See further: [[Local Search]] which is a type of informed search
## A* Search
- **Thinking Process:** Combine the cost already paid ($g$) with the estimated cost to the goal ($h$) to avoid expanding expensive paths.
- **Key Idea:** Minimize $f(n) = g(n) + h(n)$.
- **Simple Algorithm:**
    1. Place start node in Priority Queue with $f(start) = h(start)$.
    2. While queue is not empty:
        - Pop node $n$ with the lowest $f(n)$.
        - If $n$ is the goal, stop.
        - For each neighbor, calculate $g(neighbor) = g(n) + \text{cost}$.
        - Set $f(neighbor) = g(neighbor) + h(neighbor)$.
        - Add/Update neighbor in Priority Queue
    
    > The $f$-function: $f(n)$ is the estimated total cost of the path through node $n$.
    > Efficiency: A* is "optimally efficient"—no other optimal algorithm expands fewer nodes.
## Properties of Heuristics
For A* to be effective and correct, the heuristic $h(n)$ must follow specific rules.
### Admissibility
- **Key Idea:** The heuristic must never "overestimate" the cost to reach the goal. It must be optimistic.
- **Condition:** $0 \leq h(n) \leq h^*(n)$, where $h^*(n)$ is the true shortest path cost.
    > **Admissibility $\implies$ Optimality:** If $h(n)$ is admissible, A* (on tree search) is guaranteed to find the optimal solution.

### Consistency (Monotonicity)
- **Key Idea:** The estimate "quality" should stay steady or improve as you move along a path; the $f$-value should never decrease. 
- **Condition:** $h(n) \leq \text{cost}(n, a, n') + h(n')$. The estimate at $n$ is no greater than the cost to get to $n'$ plus the estimate at $n'$.
    > **Consistency $\implies$ Admissibility:** All consistent heuristics are admissible, but not all admissible heuristics are consistent. Consistency is required for A* to be optimal in **graph search** (where we revisit nodes).



