**Floyd-Warshall algorithm** computes the shortest paths between all pairs of vertices in a weighted graph, handling both positive and negative edge weights (but no negative cycles). 
- *All Pairs shortest path algorithm*
## Problem Definition
For $G = \{E, V\}$, find the shortest distance $d(i,j)$ between *every pair* of vertices $(i,j)$ in the graph. Output is a $n*n$ matrix where entry (i,j) is the shortest distance from i to j

## Algorithm Steps
1. Initialize adjacency matrix of size n x n
2. Choose a pair of `(i,j)` and for every other vertex, iterate `dp[i][j] = MIN(DVec[i][j], DVec[i][k] + DVec[k][j])`

``` al
FUNC floydsMinDistances(G)
//INPUT: G is adjacency matrix of graph with n nodes
//OUTPUT: Shortest path matrix
	FOR (i<n, i:0->n)
		FOR (j<n, i:0->n)
			FOR (k<n, i:0->n)
				G[i][j] = MIN( G[i][j], G[i][k] + G[k][j])
			END-FOR
		END-FOR
	END-FOR
RETURN G
```
## Complexity Analysis
- Time complexity = $O(n^3)$  → There are 3 loops
- Space Complexity = $O(n^2)$ → n x n matrix

> Warshall’s algorithm described whether other nodes are reachable from a given node (if there is no path (hops are allowed) from a to b, then it is set as 0)

```al
FUNC warshallsReachabillity(G)
// INPUT: Graph G of n nodes
// OUTPUT: reachability matrix
	FOR (i<n, i:0->n)
		FOR (j<n, i:0->n)
			FOR (k<n, i:0->n)
				G[i][j] = G[i][j] OR (G[i][k] AND G[k][j])
			END-FOR
		END-FOR
	END-FOR
RETURN G
```

