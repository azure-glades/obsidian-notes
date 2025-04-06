Quick sort is a comparison-based #sorting algorithm that employs the #divide-and-conquer technique. It works by selecting a pivot element, partitioning the array around it, and recursively sorting the subarrays on either side
- Time complexity
	- Best case: $O(n\log n)$. When pivot selected is always the middle element
	- Average case: $O(1.9*n\log n)$
	- Worst case: $O(n^2)$. When the list is already sorted
- Space complexity: $O(\log n)$
``` al
FUNCTION  partition(arr, low, high)
// partitions the array to prepare for sorting
// Input: arr - array to sort
// Output: index of pivot
	pivot = arr[low]
	i = low, j = high
	WHILE i<j
		DO
			i++
		WHILE arr[i] <= pivot
		DO
			j++
		WHILE arr[j] >= pivot
		IF i<j
			swap(arr[i], arr[j])
	swap(arr[low],arr[j])
RETURN j

FUNCTION quickSort(arr, low, high)
//to sort the array
//Input: arr - array to sort
//Output: array that is sorted
	IF low<high
		mid = partition(arr, low, high)
		quickSort(arr,low,mid)
		quickSort(arr,mid+1,high)
RETURN arr
```

In java
```java
class Solution {
    // Function to sort an array using quick sort algorithm.
    static void quickSort(int arr[], int low, int high) {
        if (low < high) {
            int j = partition(arr, low, high);
            quickSort(arr, low, j - 1);
            quickSort(arr, j + 1, high);
        }
    }

    static int partition(int arr[], int low, int high) {
        int pivot = arr[low];
        int i = low;
        int j = high;

        while (i < j) {
            while (i < high && arr[i] <= pivot) {
                i++;
            }
            while (arr[j] > pivot) {
                j--;
            }
            if (i < j) {
                int tmp = arr[i];
                arr[i] = arr[j];
                arr[j] = tmp;
            }
        }

        int tmp = arr[low];
        arr[low] = arr[j];
        arr[j] = tmp;

        return j;
    }
}
```