Time complexity is $O(n*m)$

```
FUNCTION matrixMultiply(m,n)
// mxn is the order of matrix
	FOR (i: 1 to n)
		FOR (j: 1 to n)
			FOR (k: 1 to n)
				result[i][j] = A[i][k]*B[k][j]
			END FOR
		END FOR
	END FOR
RETURN result
```

