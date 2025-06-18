#sorting
Recursive
```al
FUNCTION heapify(heap, size, index)
// to max heapify the tree
// Input: index of root-node
// Output: maximized heap
	max = index
	left = 2*index
	right = 2*index + 1
	IF (left<=size && heap[max]<=heap[left])
		max = left
	IF (right<=size && heap[max]<=heap[right])
		max = right
	
	IF (max != index)
		swap(heap[max], heap[index])
		heapify(heap,size,max)
RETURN

FUNCTION buildHeap(heap, size)
// turns the array to a heap
	FOR (index: size/2 -> 1)  // position 0 is ignored
		heapify(heap, size, index)
RETURN

FUNCTION heapSort(heap, size)
// sort an array using heap sort
	buildHeap(heap,size)
	FOR (n: size -> 1)
		swap(heap[1],heap[n])
		n = n-1
		heapify(heap, n, 1)  // heap[1] is root
RETURN
```

Iterative
```al
FUNCTION heapify(heap, n, i)
//INPUT: heap of size n, at current node i
	largest = i
	left = 2*i
	right = 2*i + 1
	WHILE (TRUE)
		largest = i
		IF(heap[left] > heap[largest] AND left < n)
			largest = left
		IF(heap[right] > heap[largest] AND right < n)
			largest = right
		IF(largest != i)
			tmp = heap[i]
			heap[i] = heap[largest]
			heap[largest] = tmp
			// set values for next iteration
			i = largest
			left = 2*i
			right = 2*i+1
		ELSE
			BREAK
	END WHILE
RETURN heap

FUNCTION heapSort(heap, n)
//INPUT: heap of size n
	FOR(i >= 0, i: n/2 -> 0)
		heapify(heap, n, i)
	FOR(i>0, i:n -> 0)
		tmp = heap[0]
		heap[0] - heap[i]
		sorted[n-i] = tmp
		heapify(heap,i,0)
RETURN sorted
```