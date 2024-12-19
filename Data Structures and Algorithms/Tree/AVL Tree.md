*Definition:*
A binary search tree wherein the balance factor of each node in a tree is either 0, +1, or -1
- An AVL tree is a balanced binary search tree where in worst-case to perform any binary operation takes *log(n)* time (in balanced BST, the worst case is *O(n)*)
**Balance Factor:** Height of left sub-tree - Height of right sub-tree
Ex: ![[Pasted image 20241219131904.png]]


>***The shape of a BST depends on the order of keys, hence many different shapes of BST can be produced for the same set of keys. AVL tree aims to store the set keys in the most efficient structure possible***
![[Pasted image 20241219131324.png]]

## 1. Rotations
The method of conversion of a BST to AVL tree is done using *rotations*.
***Rotations are always performed between 3 nodes***
1. Left Rotations: When the nodes are rotated/shifted towards the left of the key-node
2. Right Rotations: When the nodes are rotated/shifted towards the right of the key-node

Sometimes rotations are done in sequence to resolve imbalance.
1. Single Rotation
2. Double Rotation

To revise; [GRS](https://www.youtube.com/watch?v=O5cKauV7Kmw&list=PLtg1mdkLERgkJX3pOmHAqf-Gwp5P5PcKh&index=55) 
