> See further: Josephus Problem

Linked list is a **linear, basic, dynamic** data structure that is defined as a collection of nodes, each node containing
- information
- pointer to the next node
![[Pasted image 20241028115944.png]]

Memory for linked lists are allocated in heaps, and use [[Dynamic Memory Allocation]]. This allows the size of linked lists to be modified in run-time
> Implementation of singly linked list in C
```c
struct linked_list{
	int data;
	struct linked_list *next;
};
struct linked_list *node;
```
> Last node in a linked list points to `NULL`

## 1. Properties of linked list
- The entire list need not be moved when inserting or deleting elements between the linked list.
- Memory allocation is not contiguous
- Random access of elements of a linked list is not possible since the list has to be traversed from the beginning
- In singly linked list, traversal of array is possible only in 1 direction
	- Solved by including another pointer to the previous node. called **Doubly linked list**
	- Last node can point to the head node to make a **circular singly linked list** or **doubly linked list**
- Linked lists are a basic data structure that is used to make complex data structures like trees and maps

> **Array vs Linked list** - 8mk

| Array                                                                                               | Linked list                                                                                            |
| --------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| Static or dynamic contiguous memory allocation                                                      | Dynamic contiguous memory allocation                                                                   |
| Random access, insertion and deletion of elements via the index                                     | Sequential access based on type of linked list                                                         |
| Insertion and deletion at random place may need the elements to be shifted to fill or create spaces | Insertion and deletion at random place can be done by defining a node and linking it between the nodes |
> 6 Advantages of linked lists

## 2. Types of Linked Lists
### 2.1. [[Linear linked list]]
### 2.2. [[Circular linked list]]
### 2.3. [[Doubly linked list]]


## 3. Advantages of Linked Lists

Linked lists are a fundamental data structure in computer science, offering several advantages over traditional arrays. Here are six key benefits:

1. **Dynamic Size**: Linked lists can grow or shrink in size during runtime without the need for pre-allocated memory. This flexibility allows them to efficiently handle varying amounts of data without wasting memory on unused elements, which is often a limitation in arrays that require a fixed size at initialization[1][2].

2. **Efficient Insertions and Deletions**: In linked lists, adding or removing elements is straightforward and efficient, particularly at the beginning or end of the list. These operations typically have a time complexity of $O(1)$ as they only require updating pointers rather than shifting elements, which is necessary in arrays

3. **No Memory Wastage**: Unlike arrays, which may allocate more memory than needed (leading to wasted space), linked lists allocate memory only for the elements currently in use. This characteristic makes linked lists particularly advantageous when the total number of elements is unknown or changes frequently

4. **Flexibility in Memory Allocation**: Linked lists do not require contiguous blocks of memory; nodes can be scattered throughout memory. This feature is beneficial when working with large datasets that might not fit into a single contiguous memory space, making linked lists suitable for dynamic applications

5. **Easy Implementation of Abstract Data Types**: Linked lists serve as an excellent foundation for implementing various abstract data types such as stacks, queues, and graphs. Their inherent structure allows for straightforward management of these data types, particularly when frequent insertions and deletions are required

6. **Efficient Rearrangement**: Reordering elements within a linked list can be accomplished without moving large blocks of memory, as it only involves changing pointers. This efficiency is particularly useful in applications that require frequent updates to the order of elements

These advantages make linked lists a versatile choice for many programming scenarios, especially where dynamic data management is essential.


## 4. Applications of Linked Lists

Linked lists are versatile data structures that find applications in various fields, including operating systems and scheduling. Here are six notable applications, with three specifically related to operating systems:

1. **Job Scheduling in Operating Systems**: Linked lists are commonly used in job scheduling algorithms within operating systems. Each node in a linked list can represent a job or process, allowing for efficient management and execution of tasks. This structure facilitates the dynamic addition and removal of jobs as they are processed

2. **Memory Management**: Operating systems utilize linked lists to manage free memory blocks. When memory is allocated or freed, the system can update the linked list to reflect available memory segments, enabling efficient memory allocation and deallocation

3. **Process Control Blocks (PCBs)**: In many operating systems, linked lists are employed to maintain a list of process control blocks. Each PCB contains information about a process, such as its state, program counter, and memory allocation. Using a linked list allows the OS to easily manage multiple processes and their states dynamically

4. **Implementing Stacks and Queues**: Linked lists serve as an underlying structure for implementing stacks and queues. By using linked lists, these data structures can grow or shrink dynamically without the limitations of fixed-size arrays, making them more flexible in handling varying amounts of data

5. **Graph Representation**: Linked lists can be used to represent graphs through adjacency lists. Each node in the linked list corresponds to a vertex in the graph, with edges represented as links to other nodes. This representation is efficient for sparse graphs where the number of edges is much lower than the maximum possible

6. **Dynamic Memory Allocation**: Linked lists are utilized in dynamic memory allocation systems where memory blocks need to be allocated and deallocated at runtime. This application is crucial for programs that require variable amounts of memory during execution, enhancing efficiency and performance

These applications highlight the flexibility and efficiency of linked lists in managing dynamic data across various domains, particularly in operating systems where resource management is critical.

> Write a c program to implement a singly linked list by inserting a new node at the beginning of the linked list


