A type of Multi-way tree (*m-trees*)
2,3 Tree -> similar to a binary tree. Automatic height balanced tree
- 2 elements each node
- 3 children: 
	- left child -> less than element 1
	- middle child -> between element 1 and 2
	- right child -> greater than element 2

Height balanced trees are more efficient than BST in searching and deletions
Better than AVL trees since their overall height is lesser
### 1. Application
- Used in DBMS system
- All data is stored at leaf nodes in B tree
- B+ trees are efficient for indexing
- NTFS and BFS uses B+ tree for indexing
- EXT4 uses extent trees