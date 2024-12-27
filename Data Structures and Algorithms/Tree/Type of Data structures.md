
## Primitive and Non-Primitive DS
- Primitive DS/Basic DS: Basic data types used to store information
	EX: char, bool, int, float
- Non-Primitive DS: Collections/groups of primitive DS
	EX: array, stack, linked-list, queue, tree
## Linear and Non-linear DS
- **Linear**: Elements are stored in a sequential manner. Data elements have distinct, unique adjacent elements
	- via contiguous memory allocation or pointer/links between elements
- **Non-Linear:** Elements are not stored in a sequential manner. Data elements need not have unique adjacent elements
## 1. Arrays
- Linear data-structure where elements of a *single data type* stored in consecutive memory locations
- Elements are referred to via an **index**

- Used when storing and retrieving large amounts of similar data:

- Arrays are fixed size and cannot be changed once allocated (*Static memory allocation*)
- Contiguous memory locations may not always be available
- Insertion and Deletion is time-consuming for large array sizes. (Since parts of the array have to be shifted to make or remove spaces)

## 2. [[Linked List]]
- Linear data-structure where elements are stored in **nodes**
- Each node contains *element* and a *link to the next node*
- More memory can be allocated/elements can be stored to a list by attaching more nodes
- Linked list contains a **head** and a **tail**. LL can be read in 1 direction, or in both directions
- Tail node points to NULL

- Allows for *Dynamic memory allocation*
- Insertion-Deletion operations are *constant time*
- Searching operations are a lot slower and need more memory

## 3. [[Stack]]
- Linear data-structure where insertion and deletion of elements are done only at one end
- A stack is LIFO (last in ; first out) and is implemented with array or linked-list
- Contains:
	- `top` which stores the address of the top-most element of stack
	- `MAX` which stores the size of the stack
> if `top = NULL` stack is empty
> if `top = MAX - 1` stack is full

- Stack has 3 primitive operations:
	- `pop` to remove the topmost element
	- `push` to add an element to the top of the stack
	- `peek` to view the topmost element
>`error: stack overflow` occurs when trying to push to a full stack
>`error: stack underflow` occurs when trying to pop from an empty stack

## 4. [[Queue]]

## 5. [[Graph]]

## 6. [[Tree]]

## 7. [[Hash tables]]