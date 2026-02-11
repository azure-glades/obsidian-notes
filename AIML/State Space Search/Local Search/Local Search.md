**Local search algorithms are a type of heuristic-based search**.

**Local search algorithms** are optimization techniques that operate by iteratively improving a **single current solution** by making small, _local_ changes. They do not explore paths from the initial state to the goal; instead, they focus on finding the best possible state (the goal configuration) without recording the sequence of actions that led there.

### Key Characteristics
1. **Single State Tracking:** Unlike traditional graph-search algorithms (like 5$\text{A*}$, BFS, or DFS) that maintain and explore a search **tree** or **graph**, local search keeps track of only the **current state** (or a small set of states).
2. **Minimal Memory:** Because they don't store the path or the entire search tree, they use a **very small (often constant) amount of memory**, making them suitable for huge or continuous search spaces.
3. **Neighborhood:** The algorithm moves from the current state to a **neighboring state** by applying a minor modification (e.g., swapping two elements, changing one variable).8 The quality of the new state is measured by an **objective function** (also called a cost or fitness function).
4. **No Path:** They are used when the objective is to find the final _solution state_ itself (the optimal configuration), not the sequence of moves.

### Common Local Search Algorithms
- **Hill-Climbing Search:** Always moves to the neighboring state that offers the best improvement in the objective function (like climbing the steepest slope). It is a purely **greedy** algorithm.
- **Simulated Annealing:** An extension of Hill-Climbing that introduces randomness, allowing it to occasionally accept a "bad" (worse) move to escape **local optima**. See [[Hill-Climbing Search and Simulated Annealing]]
- **[[Local Beam Search]]:** Maintains $k$ states simultaneously and chooses the best $k$ successors from the combined pool of all their neighbors.
- **[[Genetic Algorithms]]:** An evolutionary method that works on a population of states and uses concepts like selection, crossover, and mutation to generate better solutions.

## Heuristic Based Search?
Local search algorithms rely entirely on a **heuristic** to guide their process. In this context, the heuristic is the **objective function** (or evaluation function) that is calculated for the current state and its neighbors.
- **Traditional Heuristic Search (e.g., A*):** Uses the heuristic $h(n)$ to estimate the **cost remaining** to the goal, helping to prioritize paths.
- **Local Search Heuristic:** Uses an **objective function** (let's call it $V(n)$ for "Value") to measure the **quality** of the state itself. The algorithm constantly moves in the direction of the neighbor with the best $V(n)$.

This reliance on an estimated value to make local, non-exhaustive decisions is what makes local search a powerful and practical branch of **Heuristic Search Strategies** for optimization problems.

