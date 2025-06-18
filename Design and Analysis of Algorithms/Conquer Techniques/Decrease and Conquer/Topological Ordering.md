2 methods: reverse pop order of DFS and Vertex deletion method

```al
FUNC topologicalSort(G)
	call DFS(G) -> as each vertex gets finished, insert it to linked-list
RETURN linked-list
```