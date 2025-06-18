Algorithm that finds the shortest path between two nodes
does not work if the graph has negative distance values
This is a #graph-traversal-algorithm
[Abdul Bari Dijkstra](https://www.youtube.com/watch?v=XB4MIexjvY0&list=PLL_Rr0-eLWmOMccWWU5CL_suJRjGaZdxq&index=3)

```al
FUNC dijkstraShortestPath(G, s)
//INPUT: Graph G = {V, E} and source s
//OUTPUT: shortest path vector from s
	FOR all v in V
		dist[v] = INT_MAX
		parent[v] = null
	d[s] = 0
	soln = null
	W = V
	WHILE (W != null)
		u = extractMin(W)
		soln = soln + {u}
		W = W - {u}
		FOR (v in V AND v adjacent to u)
			IF (dist[v] > dist[u] + cost(u,v))
				dist[v] = dist[u] + cost(u,v)
				parent[v] = u
			END-IF
		END-FOR
	END-WHILE
RETURN soln, dist

```