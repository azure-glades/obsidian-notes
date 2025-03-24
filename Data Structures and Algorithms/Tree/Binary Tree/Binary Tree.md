**Definition:** Every node in a binary tree has at most 2 child nodes and each sub-tree in also a binary tree
**Recursive Definition:** 
	*Base case*: A binary tree is either empty. (where root is null)
	*Recursive case*: If the tree is not empty, it consists of:
		A root node
		A left sub-tree (which is also a binary tree)
		A right sub-tree (which is also a binary tree)

> [!info]- Definitions
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


> Binary Trees are implemented in Heap memory, and are often used to implement binary search trees, expression trees, binary heaps, tournament trees.

## Types of binary tree
### 1. Strictly binary tree
*Definition:*
- A strictly binary tree or full binary tree is characterized by every node having either **zero or two children**. 
- No node can have only one child; all internal nodes must have exactly two children if they are not leaf nodes. 
- All leaf nodes are at the same level.
### 2. Complete binary tree
*Definition*:
- All levels are fully filled with nodes.
> Ex: Heaps, Cache memory
### 3. Almost complete binary tree
*Definition*:
- All levels are (except the last) fully filled with nodes
- In the last level, all leaf nodes are as leftmost as possible
### 4. Extended Binary Tree
An **extended binary tree** (also known as a **2-tree** or **full binary tree**) is a binary tree in which every non-leaf node has exactly two children, and each leaf node has two `null` or empty children.
- **Base Case**: An extended binary tree is empty or consists of a single leaf node.
- **Recursive Case**: If a node is not a leaf, it has exactly two children, both of which are also extended binary trees.
Also called a **2-Tree** or **Full binary tree**
### 5. Skewed binary tree
When all the nodes are shifted to either right or left.
### 6. [[Binary Search Tree]]
A **binary search tree (BST)** is a type of binary tree where
- Each node in the tree has at most two children.
- For every node:
    - All nodes in its left sub-tree contain values that are **less than** the value of the node.
    - All nodes in its right sub-tree contain values that are **greater than** the value of the node.
### 7. [[Expression Tree]]
An **expression tree** is a binary tree that represents a mathematical expression. In this tree:
- **Leaf nodes** (terminal nodes) represent **operands**, such as constants or variables.
- **Internal nodes** represent **operators**, such as addition (`+`), multiplication (`*`), or other mathematical functions.
The value of each tree is found by evaluating its subtrees recursively.
Evaluation of expression is dependant on order of traversal
- Preorder -> prefix expression
- Postorder -> postfix expression
- Inorder -> infix expression

### 8. [[Threaded Binary Tree]]

### 9. [[Heap]]
## Representation of binary trees
Binary trees are represented by linked lists, or as 1D arrays (which is memory inefficient).
***Linked list representation***: Each node has 3 parts, left pointer, right pointer and value
```c
struct node {
	int val;
	struct node *right;
	struct node *left;
}
```
There is also another external pointer called `root` that always points to the topmost node of a tree. 
- Empty tree is when both the pointers are `NULL`

***Sequential representation***: All values of a tree are stored in a 1D array (called `tree`). Root of the tree is stored in `tree[1]`.
```c
struct node {
	int val;
	int tree[1024];
}
```
- Children of a node are stored in `tree[2*k]` and `tree[2*k+1]` where `k` is where the parent is stored (`tree[k]`)
- Maximum size of the array is $2^{h} - 1$
- Empty tree is when value stored at `root` = `NULL`

## Deletion in BST
- Swap the element to be deleted with the rightmost node in the bottom most level
- Delete the rightmost node of the bottom most level

In BST
1. If it is leaf node, just switch with rightmost leaf and delete
2. If node has only 1 child/subtree, swap the node with its child/subtree and delete
3. If it is internal node with 2 children or subtree, find inorder successor, swap with it, and deal with the new case which is either case 1 or 2