>***A tree is recursively defined as a set of one or more nodes where one node is designated as the root of the tree and all the remaining nodes can be partitioned into sub-trees.***

> [!info]+ Definitions
> - **Root Node**: The top most node of a tree. if `root == NULL` tree doesnt exist
> - **Sub-trees**: The tree can be partitioned into sub-trees that are under the `root`. These are called sub-trees. Every node in a tree is a root to a sub-tree.
> - **Leaf Node**: The terminating node of a tree which has no children
> - **Path**: The sequence of branches taken to reach a leaf from the root
> - **Key**: Content of the node.
> 
> - **Parent Node**: The previous node above the current one -> `root` has no Parent
> - **Child Node**: The next node under the current one -> `leaf` has no Child
> - **Sibling Node**: Nodes of the same level sharing a parent node are sibling nodes.
> 
> - **Ancestor Node**: The other nodes lying on the path to root excluding the parent node
> - **Descendant Node**: The nodes that lie under the current node excluding the children nodes
> 
> - **Level Number**: Every node on a tree is assigned a number that shows how many nodes lie in the path to `root`. 
> 		- Ex: `root` is level 0
> 		- All nodes have 1 level higher than parent `level number = parent + 1`
> 		- Children of Root are level 1
> - **Depth of a tree**: The level of a node from the bottom
> - **Degree**: The number of children that a node has. A `leaf` node has degree 0
> - **In-Degree**: The number of edges leading to a node
> - **Out-Degree**: The number of edges leaving the node
> - **Height of a tree**: The total number of levels in a tree
> 	- A binary tree of height $h$ has atleast $h$ nodes and atmost $2^{h} - 1$ nodes
> 	- Similarly, a binary tree of $n$ nodes has a height of atleast $\log_{2}(n+1)$  or atmost $n$.

### Types of Trees
1. [[Binary Tree]]
2. [[Trie]]
3. [[B and B+ tree]]

### [[Tree Traversal Techniques]]