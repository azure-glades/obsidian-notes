
## 1. Implementation
### 1.1. **Node Definition and Typedef**
```c
#include <stdio.h>
#include <stdlib.h>

// Define the structure of a node in the linked list
struct node {
    int info;              // Data stored in the node
    struct node *next;     // Pointer to the next node
};

typedef struct node *NODE; // Define NODE as a pointer to the struct node
```
Defines the structure for a node in a singly linked list and creates a type alias `NODE` to simplify the code.
### 1.2. **Create a New Node**
```c
NODE getNode(int ele) {
    NODE p = (NODE)malloc(sizeof(struct node));  // Allocate memory for a new node
    p->info = ele;                              // Assign the value to the node
    return p;                                   // Return the newly created node
}
```
Creates and returns a new node containing the given integer value.
### 1.3. **Free the First Node**
```c
NODE freeNode(NODE head) {
    if (head == NULL) {                         // Check if the list is empty
        printf("List is empty\n");
        return head;
    } else {
        NODE t = head;                          // Temporary pointer to the head
        head = head->next;                      // Move the head to the next node
        printf("%d\n", t->info);                // Print the value of the removed node
        free(t);                                // Free the memory of the removed node
        return head;                            // Return the updated head
    }
}
```
Removes the first node from the list and updates the head pointer.
### 1.4. **Add a Node to the Beginning**
```c
NODE attachNode(NODE head, int ele) {
    if (head == NULL) {                         // If the list is empty
        head = getNode(ele);                    // Create the first node
        head->next = NULL;
        return head;
    } else {
        NODE p = getNode(ele);                  // Create a new node
        p->next = head;                         // Link the new node to the current head
        head = p;                               // Update head to the new node
        return head;
    }
}
```
Adds a new node with the given value at the beginning of the list.
### 1.5. **Free the Last Node**
```c
NODE freeNodeFromEnd(NODE head) {
    NODE t = head;
    if (t == NULL) {                            // If the list is empty
        printf("List is empty\n");
        return head;
    }
    while (t->next->next != NULL) {             // Traverse to the second last node
        t = t->next;
    }
    NODE q = t->next;                           // Pointer to the last node
    free(q);                                    // Free the last node
    t->next = NULL;                             // Update second last node's next to NULL
    return head;
}
```
Removes the last node in the list and ensures the second last node points to `NULL`.

### 1.6. **Add a Node to the End**
```c
NODE attachNodeAtEnd(NODE head, int ele) {
    NODE t = head;
    if (t == NULL)                              // If the list is empty, return NULL
        return head;
    while (t->next != NULL) {                   // Traverse to the last node
        t = t->next;
    }
    NODE nxt = getNode(ele);                    // Create a new node
    t->next = nxt;                              // Link the new node at the end
    nxt->next = NULL;
    return head;
}
```
Adds a new node with the given value at the end of the list.
### 1.7. **Display the List**
```c
void display(NODE head) {
    NODE t = head;
    if (t == NULL) {                            // Check if the list is empty
        printf("--- no linked list ---\n");
        return;
    }
    while (t != NULL) {                         // Traverse and print all nodes
        printf("%d -> ", t->info);
        t = t->next;
    }
    printf("[]\n");
}
``` 
Prints all the elements in the linked list in a readable format.
### 1.8. **Calculate Length of the List**
```c
int listLength(NODE head) {
    NODE mv = head;
    int count = 0;
    while (mv != NULL) {                        // Traverse and count nodes
        mv = mv->next;
        count++;
    }
    return count;                               // Return the length of the list
}
```
Counts and returns the number of nodes in the linked list.
### 1.9. **Get the Last Node**
```c
NODE getTail(NODE head) {
    NODE mv = head;
    while (mv != NULL && mv->next != NULL) {    // Traverse to the last node
        mv = mv->next;
    }
    return mv;                                 // Return the last node
}
```
Returns a pointer to the last node in the linked list.

### 1.11. Example
- [[Sparse Matrix]]
## 2. Application of singly Linked List
Singly linked lists are versatile data structures used in various applications due to their dynamic nature and efficient memory management. Here are five notable applications of singly linked lists:
1. **Web Browsers**: Singly linked lists are utilized to manage the browsing history of users. Each visited URL is stored as a node, allowing users to navigate back through their history using back and forward buttons[1][2].
2. **Music Players**: In music applications, playlists can be implemented using singly linked lists. Each song is represented as a node, enabling users to play songs sequentially or jump to the next or previous song easily[1][3].
3. **Image Viewers**: Singly linked lists facilitate navigation between images in photo viewing applications. Each image is stored as a node, allowing users to move forward and backward through their image gallery[2][4].
4. **Task Scheduling**: Operating systems often use singly linked lists for managing task scheduling. Each process waiting to be executed can be represented as a node in the list, allowing for efficient management of processes[2][4].
5. **Dynamic Memory Allocation**: Singly linked lists can be employed in dynamic memory allocation systems, where they keep track of free memory blocks. This allows for efficient allocation and de-allocation of memory as needed[3][4].

These applications highlight the flexibility and efficiency of singly linked lists in managing dynamic data across various domains.

Citations:
[1] https://www.prepbytes.com/blog/linked-list/applications-of-linked-list-data-structure/
[2] https://www.geeksforgeeks.org/applications-of-linked-list-data-structure/
[3] https://www.scaler.com/topics/application-of-linked-list/
[4] https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-linked-list/
[5] https://www.simplilearn.com/tutorials/data-structure-tutorial/linked-list-in-data-structure
[6] https://www.javatpoint.com/application-of-linked-list
[7] https://www.geeksforgeeks.org/introduction-to-stack-data-structure-and-algorithm-tutorials/
[8] https://byjus.com/gate/stack-and-its-applications/