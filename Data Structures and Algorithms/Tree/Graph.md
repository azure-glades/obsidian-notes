A graph is collection of edges and vertices i.e a Graph $G$
$$G = \{V, E\}$$ where;
	$V$ is a set of vertices
	$E$ is a set of ordered pair of vertices 

There can be many types of edges
- Parallel edges (Multiple lines connecting the same 2 vertices)
- Self loops (A line connecting a vertex to itself)
- Connected vertices (a line connecting 2 different vertices)
- Cycling (a set of lines connecting a collection of vertices)

---> called directed edges
\---- and <----->called undirected edges
- Directed Acyclic Graph
- Directed Cyclic Graph

A part of a graph is called a subgraph. 

Cyclic/Acyclic
Connected/Disconnected

A value can be associated with an edge. this is called a weight

Graphs are represented by matrices. Each row and column of a matrix represents a vertex. If edges lie between vertices that corresponding row-column is 1. else it is 0.
-  This is called an **adjacency matrix**. Adjacency matrix is always **symmetric**
If the graph is a weighted graph, weights are used instead of 1, which is called weight matrix. Sometimes can be specified as distance matrix, or cost matrix
- If 2 vertices dont have a connecting edge, it's weight is $\infty$ 
- Diagonal elements are always 0 since it is the vertex itself
Row sum is outdegree
Column sum is indegree

Graphs can also be represented as an array of linked lists. it is called **adjacency list**

Adjacency list is superior for a sparse matrix. Adjacency matrix is superior for a dense graph
