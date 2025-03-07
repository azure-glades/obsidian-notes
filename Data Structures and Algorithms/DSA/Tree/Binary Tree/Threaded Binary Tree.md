 *Definition*:
	A **threaded binary tree** is a specialized type of binary tree that enhances the efficiency of tree traversal by utilizing the null pointers typically found in standard binary trees. Instead of leaving these pointers empty, threaded binary trees replace them with "threads" that link nodes directly to their in-order predecessor or successor. This modification allows for faster traversal without the need for recursion or a stack, which is particularly beneficial for large trees.
## Key Characteristics:
1. Address fields (left or right) are used to store links when the respective child is absent:
    - **Left-threaded** stores the address of the **inorder-predecessor**.
    - **Right-threaded** stores the address of the **inorder-successor**.
2. **Full Threading**: Both left and right pointers store traversal links.
3. Each pointer has a *left flag* and *right flag* to indicate whether the link is a connection or a thread.
4. If there is no predecessor or successor, the pointer links to a **header/dummy node**:
    - The header node is unique and does not store any data.
    - Its left pointer points to the root of the tree.
    - Its right pointer points to itself.

## Classification of Threaded Binary Trees:
1. **Single threaded binary tree:** Either the Right `NULL` pointer, or the Left `NULL` pointer are replaced with threads that point to the inorder successor or predecessor
2. **Double threaded binary tree:** Both the left and right `NULL` pointers are replaced with threads that point to their inorder successor/predecessor
- Generally the predecessor/successor of thread is based on inorder. But other traversals are also acceptable and are called *Preorder TBT* and *Postorder TBT*



**Anani Leviton**.