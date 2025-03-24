self-balancing binary search tree
- guarantees searching in $O(\log n)$ time

## Rules
1. Node is either red or black
2. root and leaves (NULL nodes) are always black
3. if a node is red, its children are black
4. all paths from a node to its NULL decendents have the same number of black nodes (called the **black depth**)

- nodes need an extra bit to track color
- the longest path (farthest NULL decendent) is not more than twice the shorted path (closest NULL decendent)
	- shortest → all black nodes
	- longest → alternating red and black nodes