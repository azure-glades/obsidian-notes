**Comparison Counting Sort** is a simple #sorting sorting algorithm that sorts an array by counting the number of elements smaller than each element. The position of each element in the sorted array is determined by this count.
## Premise
- The algorithm compares each element with every other element in the array to calculate its rank (number of elements smaller than it).
- The rank is used to place each element in the correct position in the sorted array.
## Complexity
- **Time Complexity**:
  - **Best Case**: O(n²)
  - **Worst Case**: O(n²) (as it compares every pair of elements)
- **Space Complexity**: O(n) for the `count` and `sorted` arrays.
## Steps of the Algorithm
1. Initialize the Count Array
	- Create a `count` array of the same size as the input array.
	- Initialize         arr[0] = arr[i];
all elements of the `count` array to `0`.
2. Count Comparisons
	- For each element in the array, compare it with every other element.
	- If another element is smaller, increment the `count` for the current element.
3. Construct the Sorted Array
	- Use the `count` array to determine the position of each element in the sorted array.
	- Place each element at the index specified by its count in a new `sorted` array.
4. Output the Sorted Array
	- The `sorted` array now contains the elements in ascending order.

> - **Input Array**: `[4, 2, 9, 1, 6]`
> 1. Initialize the `count` array:
>    ```
>    count = [0, 0, 0, 0, 0]
>    ```
>    - Compare each element:
>      ```
>      For 4: count = 2 (elements smaller: 2, 1)
>      For 2: count = 1 (element smaller: 1)
>      For 9: count = 4 (elements smaller: 4, 2, 1, 6)
>      For 1: count = 0 (no elements smaller)
>      For 6: count = 3 (elements smaller: 4, 2, 1)
>      ```
> 2. Construct the Sorted Array:
>    ```
>    sorted[count] = [1, 2, 4, 6, 9]
>    ```
> 3. Output:
>    - Sorted Array: `[1, 2, 4, 6, 9]`

```al
FUNCTION countingSort(array, n)
	count[0 ... n]
	FOR(i<n, i:0 -> n)
		count[i] = 0
	
	FOR (i<n, i:0 -> n)
		FOR (j<n, j:0 -> n)
			IF (array[j] < array[i])
				count[i]++  
	
	FOR (i<n, i:0 -> n)
		sorted[count[i]] = array[i]
RETURN sorted
```

```c
#include <stdio.h>

// Function to perform Comparison Counting Sort
void comparisonCountingSort(int arr[], int n, int sorted[]) {
    int count[n]; // Array to store the count of elements less than each element

    // Initialize the count array to 0
    for (int i = 0; i < n; i++) {
        count[i] = 0;
    }

    // Count the number of elements less than each element
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (arr[j] < arr[i]) {
                count[i]++;
            }
        }
    }

    // Place elements in the sorted array based on the count array
    for (int i = 0; i < n; i++) {
        sorted[count[i]] = arr[i];
    }
}

int main() {
    int n;

    // Input the number of elements
    printf("Enter the number of elements: ");
    scanf("%d", &n);

    int arr[n], sorted[n];

    // Input the elements
    printf("Enter the elements:\n");
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    // Call the Comparison Counting Sort function
    comparisonCountingSort(arr, n, sorted);

    // Output the sorted array
    printf("Sorted array:\n");
    for (int i = 0; i < n; i++) {
        printf("%d ", sorted[i]);
    }
    printf("\n");

    return 0;
}
```


## Advantages
- Simple to understand and implement.
- Does not require additional data structures like heaps or trees.
## Disadvantages
- Inefficient for large arrays due to O(n²) time complexity.
- Not suitable for real-world applications involving large datasets.
## Use Cases
- Educational purposes to demonstrate basic sorting techniques.
- Situations where simplicity is preferred over efficiency.