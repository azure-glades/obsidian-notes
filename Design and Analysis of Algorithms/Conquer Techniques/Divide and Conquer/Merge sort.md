Merge sort is a stable, comparison-based #sorting algorithm that uses the #divide-and-conquer technique. It recursively divides the input array into two halves until each subarray contains a single element, then merges these subarrays in sorted order to produce the final sorted array. 
- Its time complexity is$$O(n \log n)$$ *in all cases (best, average, and worst)* making it highly efficient for large datasets.
- It requires additional space for merging, resulting in a space complexity of $O(n)$ Merge sort is particularly suitable for linked lists and scenarios where stability in sorting is required
Best, Average and Worst case: $O(n\log n)$
```al
FUNCTION merge(a, low, mid, high)
//merges unsorted into sorted arrays
//Input: a - array, low - lower index
//Output: sorted array
	i = low
	j = mid+1
	k = low
	WHILE (i<=mid AND j<=high)
		IF (a[i]<a[j])
			b[k++]  = a[i++]
		ELSE
			b[k++] = a[j++]
	
	WHILE (i <= mid)
		b[k++] = a[i++]
	WHILE (j <= high) 
		b[k++] = a[j++]
	
	FOR (i = low; i<n; i++)
		a[i] = b[i]
RETURN

FUNCTION mergeSort(a, low, high)
//sorts array using merge sort
//Input: a - array, low - lower index
//Output: sorted array
	IF (low < high)
		mid = (low + high)/2
		mergeSort(a, low, mid)
		mergeSort(a, mid+1, high)
		merge(a, low, mid, high)
RETURN
```

merge sort in c
```c
int b[64];
void mergesort(int *a, int start, int end){
	if(start < end){
		int mid = (start+end)/2;
		mergesort(a, start, mid);
		mergesort(a, mid+1, end);
	}
	merge(a, start, end);
}

void merge(int *a, int start, int end){
	if(start >= end){
		return;
	}
	int i,j,k,mid;
	k = 0;
	i = start;
	j = mid = (start+end)/2;
	while(i <= mid && j < end){
		if(a[i] < a[j])
			b[k++] = a[i++];
		else
			b[k++] = a[j++];
	}
	
	while( i <= mid)
		b[k++] = a[i++];
		
	while( j < high)
		b[k++] = a[j++];
		
	for(i = start; i < end; i++)
		a[i] = b[i-start];
}
```
here is merge sort in java
```java
void MergeSortAlgo{
    void mergeSort(int arr[], int low, int right){
       if(low < right){
           int mid = (low + right)/2;
           sort(arr, low, mid);
           sort(arr, mid+1, right);
           merge(arr, low, mid, right);
       }
    }
    
    void merge(int a[], int low, int mid, int high){
        int n1 = mid - low + 1;
        int n2 = high - mid;
        
        int[] left = new int[n1];
        int[] right = new int[n2];
        
        for(int i = 0; i<n1; ++i)
            left[i] = a[low+i];
        for(int j = 0; j<n2; ++j)
            right[j] = a[mid+1+j];
        int i = 0, j = 0, k = low;
        
        while(i < n1 && j < n2){
            if(left[i] <= right[j]){
                a[k] = left[i];
                i++;k++;
            } else {
                a[k] = right[j];
                j++;k++;
            }
        }
        
        while(i < n1){
            a[k] = left[i];
            i++;k++;
        }
        
        while(j < n2){
            a[k] = right[j];
            j++;k++;
        }
    }
}
```