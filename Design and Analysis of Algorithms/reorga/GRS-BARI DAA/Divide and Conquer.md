
## Common matrix multiplication
- General matrix multiplication for $C = A*B$
$$C_{ij} = \sum_{k=1}^{n}A_{ik}*B_{kj}$$
```algorithm
FUNCTION matrixMultiplication(A, B, n)
// multiply 2 matrices
//Input: A and B matrix and order n
//Output: Matrix C = A*B
	FOR (i:0 -> n)
		FOR (j:0 -> n)
			FOR (k:0 -> n)
				C[i][j] = A[i][k]*B[k][j]
			END FOR
		END FOR
	END FOR
RETURN C
```

## Using Divide and Conquer
1. Reduce the problem : Take a small case of 2x2 or 1x1 matrix and solve with direct formula (no loops)
2. Divide the problem

```algorithm

```
