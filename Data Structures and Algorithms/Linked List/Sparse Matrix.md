Sparse matrices are matrices where majority of entries are 0. 
For these matrices it is more memory efficient to store the data in linked lists. It would be a waste of memory to store them as as an array since we would allocate a huge amount of memory storing 0s.


Implementation as a linked list
```c
struct entry {
	int column;
	int row;
	int info;
	pointer next;
}
```
header node is unique: stores the number of non-zero elements and size of the sparse matrix
```c
struct entry *head;
head->info = number-of-non-zero-entries
head->row = size-of-matrix
head->column = size-of-matrix
```
