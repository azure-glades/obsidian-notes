***Addition of Long positive integers using circular linked list***
- Represent long integers as groups of normal integers
- Represent them as a linked list

## Recursive function to find greatest element in binary tree
Compare left child with right child.
- if left child is greater, move to left subtree
- if right child is greater, move to right subtree
```c
int findMax(NODE root)
{
	if(root = NULL)
		return -1;
	if(root->left == NULL && root->right == NULL)
		return root->val;
	leftmax = findMax(root->left);
	rightmax = findMax(root->right);
	if(leftmax > rightmax)
		max = leftmax;
	if(root->val > max)
		return root->val;
	else
			return max;
}
```
