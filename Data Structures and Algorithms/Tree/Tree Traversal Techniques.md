## 1. In-order (L root R)
1. Visit Left subtree recursively
2. Check root
3. Visit right subtree recursively
**The output of elements is sorted in ascending order**
*Implementation in C:*
```c
struct node {
	int key;
	struct node *left;
	struct node *right;
};
struct node *root;

void inorder(struct node *root)
{
	if(root == NULL)
		return;
	inorder(root->left);
	printf("%d\t", root->key);
	inorder(root->right);
}
```

## 2. Pre-order (root L R)
1. Check root
2. Visit Left order
3. Visit right subtree
```c
void preorder(struct node *root)
{
	if(root == NULL)
		return;
	printf("%d\t", root->key);
	preorder(root->left);
	preorder(root->right);
}
```
## 3. Post order (L R root)
1. Visit Left subtree
2. Visit right subtree
3. Check root
```c
void postorder(struct node *root)
{
	if(root == NULL)
		return;
	postorder(root->left);
	postorder(root->right);
	printf("%d\t", root->key);
}
```
## 4. Level order
