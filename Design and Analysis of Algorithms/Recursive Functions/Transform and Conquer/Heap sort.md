#sorting
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