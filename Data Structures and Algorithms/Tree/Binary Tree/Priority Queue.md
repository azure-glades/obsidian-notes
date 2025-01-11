A **priority queue** is a type of data structure where each element has a priority associated with it, and elements with higher priority are processed before those with lower priority
- Most commonly seen in ready-queue in priority-based scheduling algorithm

## Advantage
1. **Efficient Sorting of Tasks**: Priority queues are great when you need to handle tasks in order of importance, like in scheduling systems, simulations, or network traffic management.
2. **Dynamic Behavior**: Unlike sorted arrays, a priority queue can handle inserting new elements and retrieving the highest priority one efficiently.

## Heap vs Stack for implementation
A **heap** is the perfect backend for implementing a priority queue because:
- **Fast Access to the Max/Min Element**: In a heap, the maximum (or minimum) element is always at the root, making retrieval super quick (O(1)).
- **Efficient Insertions and Deletions**: Heaps maintain their structure dynamically with insertions and deletions in O(log n) time, thanks to their tree-like structure.
- **Space Optimization**: Heaps are also space efficient when implemented through an array

In contrast, a **regular array** would need to be sorted to keep priorities in order. This means:
- **Sorting Overhead**: If you insert an element into an unsorted array, you’d need O(n) to find its correct position and sort the array again.
- **Inefficient Deletions**: Removing the highest priority element in an unsorted array also takes O(n), as you’d have to search through all elements.

Using a heap for a priority queue is like having a perfectly ordered to-do list where urgent tasks naturally bubble up to the top

```c
#include <stdio.h>
#include <stdlib.h>

// Function to heapify the array to maintain max-heap property
void heapify(int a[10], int n)
{
    int i, k, v, j, flag = 0;

    // Start from the last non-leaf node and heapify each subtree
    for (i = n / 2; i >= 1; i--)
    {
        k = i;         // Current node index
        v = a[k];      // Value at the current node
        flag = 0;      // Reset flforag for each subtree

        // Maintain heap property in the subtree rooted at 'k'
        while (!flag && 2 * k <= n) // Check if the node has children
        {
            j = 2 * k; // Left child index

            // Find the larger child, if any
            if (j < n && a[j]v < a[j + 1])
                j = j + 1;

            // If the current node is larger or equal, stop
            if (v >= a[j])
                flag = 1;
            else
            {
                a[k] = a[j]; // Swap current node with the larger child
                k = j;       // Move to the next level
            }
        }

        a[k] = v; // Place the value at the correct position
    }
}

void main()
{
    int n, i, a[10], ch;

    // Menu-driven program for priority queue operations
    while (1)
    {
        printf("create/extract max/exit\n> ");
        scanf("%d", &ch);

        switch (ch)
        {
            case 1: // Create a heap
                printf("# ");
                scanf("%d", &n); // Read number of elements
                printf("IN:\n");
                for (i = 1; i <= n; i++) // Input elements
                    scanf("%d", &a[i]);
                heapify(a, n); // Convert array to max-heap
                printf("Heap: \n");
                for (i = 1; i <= n; i++) // Display the heap
                    printf("%d\t", a[i]);
                break;

            case 2: // Extract max (highest priority)
                if (n >= 1)
                {
                    printf("MAX DELETED: %d\n", a[1]); // Remove root
                    a[1] = a[n]; // Replace root with the last element
                    n = n - 1;   // Reduce size
                    heapify(a, n); 
                    // Reheapify to maintain max-heap property
                    if (n != 0) // Display the updated heap
                    {
                        printf("NEW HEAP: ");
                        for (i = 1; i <= n; i++)
                            printf("%d\t", a[i]);
                    }
                }
                else
                    printf("\nHeap empty");
                break;

            default: // Exit the program
                exit(0);
        }
    }
}

```