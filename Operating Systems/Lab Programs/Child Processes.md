[[Lab Programs]]
### Main Function (Process Creation):

```c
#include <stdio.h>
#include <string.h>
#include <sys/types.h>
#include <stdlib.h>
#include <unistd.h>
#include <wait.h>

int main(int argc, char *argv[]) {
    printf("Main Function: \n");
    int retval = 1; // Variable to store the return value of the child process
    pid_t pid = fork(); // Create a child process

    if (pid < 0) {
        // If fork() returns a negative value, the creation of the child process failed
        printf("Error in fork operation\n");
        exit(1);
    }

    if (pid == 0) {
        // This block is executed by the child process
        printf("PID for Child process: %d\nPID of its parent process: %d\n", getpid(), getppid());
        // Replace the child process with a new program (binary search application)
        execl("./binsearch", argv[1], NULL);
    } else {
        // This block is executed by the parent process
        printf("PID of parent process: %d\n", getpid());
        // Wait for the child process to complete
        wait(&retval);

        // Check if the child process terminated normally
        if (WIFEXITED(retval) == 1) {
            printf("Child terminated normally\n");
        } else {
            printf("Child terminated abnormally\n");
            exit(0);
        }
    }

    return 0;
}
```

### Binary Search Application:

```c
#include <stdio.h>

// Function to perform binary search on a sorted array
int binarySearch(int arr[], int l, int r, int x) {
    if (r >= l) {
        int mid = l + (r - l) / 2;
        
        // Check if the target element is present at the mid index
        if (arr[mid] == x)
            return 1;
        
        // If the target element is smaller than the mid element, search the left subarray
        if (arr[mid] > x)
            return binarySearch(arr, l, mid - 1, x);
        
        // If the target element is larger than the mid element, search the right subarray
        return binarySearch(arr, mid + 1, r, x);
    }
    
    // Return -1 if the target element is not found in the array
    return -1;
}

// Function to swap two elements
void swap(int *xp, int *yp) {
    int temp = *xp;
    *xp = *yp;
    *yp = temp;
}

// Function to sort the array using bubble sort
void sort(int arr[], int n) {
    int i, j;
    for (i = 0; i < n - 1; i++)
        for (j = 0; j < n - i - 1; j++)
            if (arr[j] > arr[j + 1])
                swap(&arr[j], &arr[j + 1]);
}

// Main function to read input, sort the array, and perform binary search
int main(void) {
    int n, key, arr[10];
    
    // Read the number of elements in the array
    printf("Enter the number of elements in the array: ");
    scanf("%d", &n);
    
    // Read the elements of the array
    printf("Enter the elements: ");
    for (int i = 0; i < n; i++)
        scanf("%d", &arr[i]);
    
    // Sort the array
    sort(arr, n);
    
    // Read the element to be searched
    printf("Enter element to be searched: ");
    scanf("%d", &key);
    
    // Perform binary search
    int result = binarySearch(arr, 0, n - 1, key);
    
    // Print the result of the binary search
    if (result == -1)
        printf("Element is not present in array\n");
    else
        printf("Element is present\n");
    
    return 0;
}
```

### Explanation:
1. **Main Function (Process Creation)**
   - The `main` function creates a new process using `fork()`.
   - If `fork()` fails, it prints an error message and exits.
   - If `fork()` succeeds, it creates a child process.
   - The child process prints its PID and its parent's PID, then replaces its program with the binary search application using `execl()`.
   - The parent process waits for the child process to complete and checks if it terminated normally, printing an appropriate message.

2. **Binary Search Application:**
   - The `binarySearch` function performs a binary search on a sorted array.
   - The `swap` function swaps two elements in the array.
   - The `sort` function sorts the array using bubble sort.
   - The `main` function reads the number of elements and the elements of the array from the user, sorts the array, and then performs a binary search for the specified element, printing whether or not the element is present in the array.

These comments should help a student understand the flow of the program and how process creation and binary searching are implemented.