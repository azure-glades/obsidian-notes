The **Bellman-Ford algorithm** is a *single-source shortest-path algorithm* for weighted directed graphs. It computes the shortest paths from a starting vertex to all other vertices, accommodating graphs with **negative edge weights** (unlike Dijkstra’s algorithm). However, it cannot produce valid results if a **negative cycle** (a cycle where the total edge weight is negative) is reachable from the source

## Premises
- **Handles negative weights**: Unlike Dijkstra’s, it works with graphs containing edges with negative weights
- **Detects negative cycles**: It identifies if a negative cycle exists, making the shortest-path problem unsolvable
- **Dynamic programming approach**: Uses iterative relaxation to refine distance estimates
## Time Complexity
- **Worst/Average case**: $O(V⋅E)$, where V = number of vertices, E = number of edges
- **Best case**: $O(E)$ if the solution is found in one relaxation pass (e.g., in sparse graphs)
- Slower than Dijkstra’s $O(E+V\log V)$  but more versatile
## Algorithm
[Abdul Bari on Bellman-Ford](https://www.youtube.com/watch?v=FtN3BYH2Zes)

## Advantages
- Handles negative weight edges
- Detects negative weight cycles
- Simple and intuitive to implement
- Suitable for dynamic graphs and distributed systems (e.g., network routing)
- Can work with both directed and undirected graphs (with caution)

## Disadvantages
- Slower than Dijkstra’s algorithm (`O(V × E)`)
- High memory usage for large graphs
- Inefficient for graphs without negative weights
- Requires `V-1` iterations, which can be computationally expensive
- Not ideal for real-time systems

## Use Cases
- **Network Routing:** Used in RIP (Routing Information Protocol)
- **Urban Planning:** Road network design
- **Robotics:** Navigation and pathfinding
- **Finance:** Portfolio optimization, risk minimization

```al
FUNCTION bellman_ford(adj_matrix, vertices)
//INPUT adjacency matrix of nxn, list of n vertices
//OUTPUT: list of shortest paths
	FOR(v: vertices)
		v = INT_MAX
	v[0] = 0  //starting vertex is 0, shortest path from 0
	n = vertices.LENGTH
	FOR(k<n-1, k:0 -> n-1)
		FOR(i<n, i:0 -> n)
			FOR(j<n, j:0 -> n)
				IF(adj_matrix[i][j] != INT_MAX) 
				AND (vertices[i] != INT_MAX) 
				AND (vertices[i] + adj_matrix[i][j] < vertices[j])
					vertices[j] = vertices[i] + adj_matrix[i][j]
				END-IF
			END-FOR
		END-FOR
	END-FOR
RETURN vertices
```

```c
#include <stdio.h>
#include <limits.h> // For INT_MAX

#define NADA INT_MAX

void bellman_ford(int adjmatrix[][4], int *vertices, int n) {
    // Initialize distances to infinity
    for (int i = 0; i < n; i++) {
        vertices[i] = NADA;
    }
    vertices[0] = 0; // Start vertex distance is 0

    // Relax edges (n-1) times
    for (int k = 0; k < n - 1; k++) {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (adjmatrix[i][j] != NADA && vertices[i] != NADA && 
                    vertices[i] + adjmatrix[i][j] < vertices[j]) {
                    vertices[j] = vertices[i] + adjmatrix[i][j];
                }
            }
        }
    }
}

int main() {
    // Define the adjacency matrix
    int adjmatrix[4][4] = {
        {0, 2, 5, NADA},
        {NADA, 0, 3, NADA},
        {NADA, NADA, 0, 4},
        {NADA, NADA, NADA, 0}
    };
    int n = 4; // Number of vertices
    int vertices[4]; // To store shortest distances

    // Call the Bellman-Ford algorithm
    bellman_ford(adjmatrix, vertices, n);

    // Print the shortest distances
    printf("Shortest distances from vertex 0:\n");
    for (int i = 0; i < n; i++) {
        if (vertices[i] == NADA) {
            printf("Vertex %d: INF\n", i);
        } else {
            printf("Vertex %d: %d\n", i, vertices[i]);
        }
    }

    return 0;
}
```