
*Definition*:
A queue is a linear data structure that operates on the First In, First Out (FIFO) principle.
- Basic operations are *enqueue* and *dequeue*
- A basic queue always *adds elements to its end* and *removes elements from the front*
## Types of Queues
- [[Linear Queue]]: Elements are connected in a sequential, linear manner
- [[Circular Queue]]:
		- EX: Task scheduling
	- memory allocation
	- round-robin algorithm
	- managing data-packets in network
- **priority queue**:
	- EX: Data compression algorithms (like *Huffman coding*)
	- network routing *(A\* search algorithm)*
- **d.e queue**  (double ended queue) Queue can be used to add or remove elements from both ends. d.e queue can be input restricted, or output restricted 
	- EX: to check if a string is a palindrome
	- browser-history
- **concurrent queue**: thread-safe queue designed to handle multiple operations from different processes
	- Event driven programming for network messaging/input arrangement
- **blocking queue**: a type of queue that waits for itself to become non-empty before retrieving an element, and waits for the space to become available before storing an element. 

## Application of Queues
- FIFO (first in first out) order of elements
- Producer-Consumer problems
- Sliding window problem
- Breadth-first search (BFS)
- Graph Traversal algorithm