Time Complexity: $O(n^2)$

```algorithm
FUNCTION distinctCheck(A, size)
//Input: A is array to check. size is the size of array\
//Output: 
	FOR (i: 1 -> size)
		FOR(j: 1 -> size)
			IF A[i] = A[j]
				RETURN False
RETURN True
```
