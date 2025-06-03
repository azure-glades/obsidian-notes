#graph-traversal-algorithm
Prim's algorithm constructs an [[Minimum Spanning Tree]] by iteratively adding the shortest available edge that connects a vertex in the MST to a vertex outside it. It was first developed by Vojtěch Jarník in 1930 and later rediscovered by Robert Prim and Edsger Dijkstra.
## Key Premise
- The algorithm uses a greedy approach: at each step, it selects the edge with the smallest weight that expands the MST to include a new vertex. → Greedy approach
- This ensures the total weight of the spanning tree remains minimized.
## Steps in Prim's Algorithm
1. **Initialize**
    - Select an arbitrary starting vertex and add it to the MST.
    - Track vertices in the MST (`visited`) and those not yet included (`unvisited`).
2. **Find Minimum-Weight Edge**
    - Identify the edge with the smallest weight that connects a vertex in `visited` to one in `unvisited`.
3. **Expand the MST**
    - Add the selected edge and its destination vertex to the MST.
4. **Repeat**
    - Continue steps 2–3 until all vertices are included in the MST.

**Key Data Structures:**
- *Priority queue (min-heap)* efficiently selects the minimum-weight edge.
- Arrays to track edge weights and parent vertices.

```al
ALGO primsMinSpanningTree(G)
// INPUT: Graph G = {V, E} of n nodes
// OUTPUT: Spanning Tree T = {V, E'}
	E' = {}
	PriorityQueue Ep = {}
	i = 0
	FOR(i<n, i:0 -> n)
		FOR(j<n, j: 0 -> n)
			IF(E[i][j] != 0)
				Ep.INSERT(E[i][j])  // insert edge to priority queue
			END-IF
		END-FOR
		MinEdge = Ep.POP()
		E' = E' + {MinEdge}

// ALGO IS INCOMPLETE --> FINISH IT
```

## Time Complexity

| Implementation                  | Time Complexity | Best Use Case    |
| ------------------------------- | --------------- | ---------------- |
| Adjacency Matrix                | O(V^2)          | Dense Graphs     |
| Adjacency List + Min-Heap       | O(E log V)      | Sparse Graphs    |
| Adjacency List + Fibonacci Heap | O(E + V log V)  | Theoretical Best |
>[!note]+ Fibonacci Heap
>- **Min-heap property**: Each tree’s root has the minimum key in its subtree.
>- **Lazy merging**: Consolidation of trees is deferred until necessary (e.g., during `extract-min`).
>- **Amortized efficiency**: Most operations (except `delete-min`) run in constant time
## Applications
- Communication network design (e.g., laying cables with minimal cost)
- Urban planning and electrical grids
- Cluster analysis in machine learning
- Maze generation using weighted grids
- Pathfinding and robotics
- Social network analysis

Prim's algorithm is particularly efficient for dense graphs and guarantees an optimal solution under the greedy framework. Its performance depends on the choice of data structures for edge selection.