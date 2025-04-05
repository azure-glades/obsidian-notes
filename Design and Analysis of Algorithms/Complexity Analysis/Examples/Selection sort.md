#sorting
Best, Worst and Average case is $O(n^2)$

```algorithm
FUNCTION selectionSort(arr, size)
// sort the array
//Input: arr - array, size
//Output: arr - sorted array
	FOR(i: 0 -> size-1)
		min = i
		FOR (j: i+1 -> size-1)
			IF arr[min] > arr[j]
				min = j
			END IF
		END FOR
		IF min != i
			swap(a[min],a[i])
		END IF
RETURN
```

