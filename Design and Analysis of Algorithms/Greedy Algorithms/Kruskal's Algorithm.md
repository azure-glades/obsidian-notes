#graph-traversal-algorithm
Kruskal's algorithm constructs an [[Minimum Spanning Tree]] by iteratively adding the smallest available edge that does not form a cycle in the current MST. It was developed by Joseph Kruskal in 1956 and operates on the principle of sorting edges by weight.
## Key Premise
- Uses a **greedy approach**: Always selects the smallest-weight edge that does not create a cycle.
- Relies on **Union-Find (Disjoint Set Union)** data structure to efficiently detect cycles.
## Steps in Kruskal's Algorithm
1. **Sort Edges**
    - Arrange all edges in ascending order of their weights.
2. **Initialize MST**
    - Create an empty set to store MST edges.
    - Initialize a Union-Find structure where each vertex is its own parent.
3. **Process Edges**
    - Iterate through sorted edges.
    - For each edge:
        - Check if its endpoints belong to different sets using Union-Find.
        - If **no cycle** is detected, add the edge to the MST and merge the sets.
4. **Terminate**
    - Stop when the MST contains $V-1$ edges (where $V$ = number of vertices).
## Time Complexity

| **Component**         | **Complexity**    |
| --------------------- | ----------------- |
| Edge Sorting          | $O(E * \log E)$   |
| Union-Find Operations | $O(E * \alpha(V)$ |
| **Total**             | $O(E * \log E)$   |
  
- $\alpha$ : Inverse Ackermann function (nearly constant).
## Applications
- Designing **low-cost networks** (e.g., roads, telecom).
- **Circuit board wiring** to minimize total connection length
- **Cluster analysis** in machine learning.
- **Approximation algorithms** for NP-hard problems.
## Comparison with Prim's Algorithm

| **Feature**         | Kruskal's Algorithm       | Prim's Algorithm |
| ------------------- | ------------------------- | ---------------- |
| **Approach**        | Edge-based                | Vertex-based     |
| **Best For**        | Sparse graphs             | Dense graphs     |
| **Data Structure**  | Union-Find + Sorted Edges | Priority Queue   |
| **Time Complexity** | $O(E * \log E)$           | $O(E* \log V)$   |

Kruskal's algorithm is preferred for graphs with many vertices and sparse edges due to its efficient cycle detection and sorting step.