The **Distribution Sorting Algorithm** is a non-comparison-based sorting technique that sorts elements by counting the frequency of each distinct element and then reconstructing the sorted array. It is particularly efficient for sorting integers or categorical data with a small range of values.
## Premise
- The algorithm relies on the assumption that the data to be sorted comes from a small, finite range of integers.
- It avoids the need for comparisons by leveraging a **counting array** to store the frequency of each element.
- The sorted order is achieved by iterating over the counting array and reconstructing the original array in ascending order.
## Steps of the Algorithm
1. Find the Maximum Value: Traverse the array to find the maximum value. This determines the size of the counting array (range of the input values).
2. Create and Populate the Count Array
	- Create a count array of size `max + 1`, initialized to zero.
	- Traverse the input array and increment the count of each element in the count array.
3. Reconstruct the Sorted Array
	- Iterate over the count array.
	- For each non-zero count, add the corresponding element to the original array as many times as its count.
4. Output the Sorted Array
	- The original array is now sorted in ascending order.
> Ex: **Input Array**: `[4, 2, 2, 8, 3, 3]`
> 1. Find the maximum value:
>    - Maximum = `8`
> 2. Create and populate the count array:
>    `Count Array: [0, 0, 2, 2, 1, 0, 0, 0, 1]`
> 3. Reconstruct the sorted array:
>    - Sorted Array: `[2, 2, 3, 3, 4, 8]`
> **Output Array**: `[2, 2, 3, 3, 4, 8]`
## Complexity
- **Time Complexity**:
  - **Best Case**: O(n)
  - **Worst Case**: O(n + k), where `k` is the maximum value in the array (size of the range).
- **Space Complexity**: O(k), where `k` is the size of the count array.

```al
FUNCTION distributionSort(array, n)
//INPUT: n is size of array
	max = MAX(array)  //max element in array
	count[0 ... max]  // count array to store counts
	FOR(i < n, i:0 -> n)
		count[array[i]]++;
	index = 0
	FOR(i<=max, i:0->max)
		WHILE(count[i]>0)
			array[index++] = i
			count[i]--;
RETURN array
```

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Function to find the maximum value in an array
int findMax(int arr[], int n) {
    int max = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }
    return max;
}

// Distribution Sort (similar to Counting Sort)
void distributionSort(int arr[], int n) {
    // Find the maximum value in the array to determine the range
    int max = findMax(arr, n);

    // Create the count array and initialize to zero
    int *count = (int *)calloc(max + 1, sizeof(int));

    // Count the occurrences of each element
    for (int i = 0; i < n; i++) {
        count[arr[i]]++;
    }

    // Reconstruct the sorted array using the count array
    int index = 0;
    for (int i = 0; i <= max; i++) {
        while (count[i] > 0) {
            arr[index++] = i;   // since we traverse the array in smallest to largest, index i stores the elements of the array
            count[i]--;
        }
    }

    // Free the dynamically allocated memory
    free(count);
}

int main() {
    int n;

    // Input the number of elements
    printf("Enter the number of elements: ");
    scanf("%d", &n);

    // Input the elements
    int arr[n];
    printf("Enter the elements:\n");
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    // Call the distribution sort function
    distributionSort(arr, n);

    // Output the sorted array
    printf("Sorted array:\n");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");

    return 0;
}


```
## Advantages
- Extremely efficient for sorting integers or categorical data with a small range of values.
- Runs in linear time for small ranges.
## Disadvantages
- Requires additional space for the counting array.
- Not suitable for sorting data with a large range of values.
- Cannot sort data with non-integer keys or floating-point numbers without additional modifications.
## Use Cases
- Sorting small ranges of integers.
- Frequency analysis in data processing.
- Applications where the range of input values is known and limited.