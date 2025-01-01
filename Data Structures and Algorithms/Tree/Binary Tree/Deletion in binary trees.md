- Swap the element to be deleted with the rightmost node in the bottom most level
- Delete the rightmost node of the bottom most level

In BST
1. If it is leaf node, just switch with rightmost leaf and delete
2. If node has only 1 child/subtree, swap the node with its child/subtree and delete
3. If it is internal node with 2 children or subtree, find inorder successor, swap with it, and deal with the new case which is either case 1 or 2

