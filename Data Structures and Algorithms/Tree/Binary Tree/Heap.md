**Definition**: A binary tree that satisfies two properties
- Structural Property: Tree is an almost complete binary tree (All levels except the last are fully filled with nodes, and all leaf nodes are left-most)
- Parental Dominance: The info stored in the parent node is dominates that of its children. (The value in the parent is either greater than children (*max heap*), or is lesser than children (*min heap*))
![[Pasted image 20241219160928.png]]
![[Pasted image 20241219161000.png]]


### 1. Heapification
The construction of a heap is called **heapification**. Both the methods need not produce the same heap.
1. Bottom-up approach:
	- Create a binary tree.
	- Go from bottom nodes comparing all parent nodes and switching to maintain property. Recursively apply to subtrees when switching is done
2. Top-down approach
	- Add nodes
	- Keep checking parental dominance as each node gets added
	- If a switching is done, recursively check for upper and lower subtrees

> Q. Construct a max heap and min heap for 5,8,7,6,10,4,1 using bottom up approach and top down approach


### 2. Application of Heaps
1. [[Priority Queue]]