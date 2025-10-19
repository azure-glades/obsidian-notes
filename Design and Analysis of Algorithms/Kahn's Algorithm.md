#graph-traversal-algorithm
![](https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png)

**Kahn's Algorithm for Topological Ordering**

**Key Premise** Kahn's algorithm is a method for obtaining a topological order of a Directed Acyclic Graph (DAG). The core idea is to iteratively remove nodes with no incoming edges (in-degree zero), ensuring for every directed edge $u \rightarrow v$, node $u$ appears before $v$ in the output order. If the graph contains a cycle, a topological ordering is impossible.[^1](https://en.wikipedia.org/wiki/Topological_sorting)[^3](https://fahadsultan.com/csc223/datastructs/graphs_topo_kahn.html)

**Algorithm Steps**

1. **Calculate In-Degree:** For each node, count the number of incoming edges (in-degree).[^3](https://www.geeksforgeeks.org/dsa/topological-sorting-indegree-based-solution/)
2. **Initialize Queue:** Place all nodes with in-degree zero into a queue or another suitable structure.[^2](https://www.geeksforgeeks.org/dsa/kahns-algorithm-vs-dfs-approach-a-comparative-analysis/)[^1](https://www.geeksforgeeks.org/dsa/topological-sorting-indegree-based-solution/)
3. **Processing:** While the queue is not empty:
    - Remove a node from the queue and append it to the topological order list.
    - For each neighbor linked by an outgoing edge, decrease its in-degree by one.
    - If a neighbor’s in-degree becomes zero, add it to the queue.[^4](https://codeanddebug.in/blog/topo-sort-kahns-algorithm/)[^1](https://interviewkickstart.com/blogs/learn/kahns-algorithm-topological-sorting)
4. **Cycle Detection:** After processing, if the number of nodes in the result doesn't match the original graph, a cycle exists, and no topological order is possible.[^1](https://interviewkickstart.com/blogs/learn/kahns-algorithm-topological-sorting)[^4](https://fahadsultan.com/csc223/datastructs/graphs_topo_kahn.html)

**Pseudocode**

```python
function topologicalSort(graph):
	    in_degree = [0 for _ in graph]            # Step 1: Initialize in-degree array
    for u in graph:
        for v in graph[u]:
            in_degree[v] += 1                # Count all in-degrees

    queue = [u for u in graph if in_degree[u] == 0]   # Step 2: Collect all nodes with zero in-degree
    topo_order = []                           # List to store the result

    while queue:
        u = queue.pop(0)                     # Remove from queue
        topo_order.append(u)
        for v in graph[u]:
            in_degree[v] -= 1                # Remove edge
            if in_degree[v] == 0:
                queue.append(v)

    if len(topo_order) == len(graph):
        return topo_order                    # Valid topological sort
    else:
        return "Graph has a cycle"           # No topological order possible
```

(Also found in C/C++/Java variants. Order of elements may vary based on data structure used.)[^2](https://interviewkickstart.com/blogs/learn/kahns-algorithm-topological-sorting)[^4](https://fahadsultan.com/csc223/datastructs/graphs_topo_kahn.html)

**Time Complexity**

- **O(V + E)**, where V is the number of vertices and E is the number of edges.
    - Calculating in-degrees for all nodes: $O(E)$
    - Each vertex is enqueued and dequeued at most once: $O(V)$
    - Each edge is processed once when reducing in-degrees: $O(E)$[^7](https://heycoach.in/blog/kahns-algorithm/)[^9](https://interviewkickstart.com/blogs/learn/kahns-algorithm-topological-sorting)[^4](https://www.geeksforgeeks.org/dsa/topological-sorting-indegree-based-solution/)[^2](https://en.wikipedia.org/wiki/Topological_sorting)

**Space Complexity**

- **O(V)**, due to storage for in-degree array, result list, and queue.[^3](https://fahadsultan.com/csc223/datastructs/graphs_topo_kahn.html)

**Applications**

- **Task Scheduling:** Sequence tasks with dependencies so that prerequisites are always completed first.[^10](https://heycoach.in/blog/kahns-algorithm/)
- **Build Systems and Compilation:** Resolve compilation order of modules or source files with dependency chains (as in software build systems).[^8](https://www.numberanalytics.com/blog/unlocking-kahn-algorithm-graph-theory)
- **Course Scheduling:** Order classes so all prerequisites are met (common in academic planners).[^1](https://www.geeksforgeeks.org/dsa/topological-sorting-indegree-based-solution/)
- **Dependency Resolution:** Used in OS package managers and database operations.[^10](https://heycoach.in/blog/kahns-algorithm/)
- **Data Processing Pipelines:** Organize operations where some processing steps depend on output from others.[^10](https://www.numberanalytics.com/blog/unlocking-kahn-algorithm-graph-theory)

**Summary Table**

| Aspect              | Details                                                          |
| ------------------- | ---------------------------------------------------------------- |
| **Premise**         | Remove indegree-zero nodes, updating neighbors, for DAGs         |
| **Steps**           | Calculate in-degree, queue zero in-degree nodes, process, repeat |
| **Time Complexity** | $O(V + E)$                                                       |
| **Main Use Cases**  | Scheduling, builds, dependencies, course planning                |
| **Cycle Detection** | Fails if a cycle exists (not a DAG)                              |

⁂