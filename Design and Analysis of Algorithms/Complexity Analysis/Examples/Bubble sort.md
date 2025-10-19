#sorting

Best case : $O(n)$ when array is sorted
Worst and Average case: $O(n^2)$
```algorithm
FUNCTION bubbleSort(arr, size)
	FOR (i: 0 -> size-1)         // n iterations, but index from 0 to n-1
		FOR (j: 0 -> size-i-1)
			IF (a[j]>a[j+1])
				swap(a[j], a[j+1])
			END IF
		END FOR
	END FOR
RETURN
```
