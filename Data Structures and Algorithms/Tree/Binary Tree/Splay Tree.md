*Definition*:
	A self adjusting (organizing) Binary Search Tree where the most recently accessed key (element) is the root node
	It is not a strictly balanced BST

- After performing an insertion, deletion or search operation, a rotation operation has to be performed (called a splay operation)
	- This splay operation makes the recently accessed key as the root node

### 1. Splay Operations
After every access (search, insertion, or deletion), the accessed node is moved to the root of the tree through a series of rotations known as "splaying."  It is a type of rotation operation
Unlike traditional balanced trees like AVL or Red-Black trees, splay trees do not maintain strict balance. Instead, they adjust dynamically based on access patterns, which can lead to better performance for certain sequences of operations

> Visualize how the nodes move. Goal is to move the key to the top, so see what path it takes. The directions it needs to move is your Zig and Zag operations
1. **Zig operation (Right rotation)**
2. **Zag operation (Left rotation)**
3. **Zig-Zig (RR rotation)** : When the key is the right child and right grandchild. Zig-Zig is performed on the grandparent node
4. **Zag-Zag (LL rotation)**: When the key is the left child and left grandchild. Zag-Zag is performed on the grandparent node
5. **Zig-Zag (RL rotation)**:
6. **Zag-Zig(LR rotation)**

### 2. Insertion Deletion


### 3. Application
1. Most obvious application: Cache memory
2. Network routing table
3. Virtual memory management