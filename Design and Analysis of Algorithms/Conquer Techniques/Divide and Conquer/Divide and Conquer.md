%%Explain what is divide and conquer and what it is used for%%
 A problem-solving strategy that involves breaking a complex problem into smaller, more manageable subproblems, solving each subproblem independently (often recursively), and then combining their solutions to address the original problem.
- **Divide**: Break the problem into smaller parts.
- **Conquer**: Solve each part recursively or directly.
- **Combine**: Merge solutions of subproblems.

When dividing into subproblems, if 2 or more subproblems are made, it is divide and conquer. 
If only a single subproblem , then it is common referred as [[Decrease and Conquer]].
Advantage:
- Simplifies complex problems.
- Efficient memory usage.
- Suitable for parallel processing.

> Examples:
> [[Merge sort]] - Found by John von Neumann
> [[Quick sort]]
> [[Heap sort]]
> [[Radix Sort]]
> [[Counting Sort]]
> [[Distribution Sort]]
> Famous algorithms
> [[Strassen's Matrix Multiplication Algorithm]]
> [[Karatsuba Multiplication]]
> [[Marching Cubes Algorithm]]
> Fibonnaci numbers (normal recurrence, not divide-conquer)
> Chip testing problem (pg 122)
> Monge Arrays
> Cooley-Tuckey FFT
> [[Barnes-Hut Algorithm (DAA LAB EL)]]
> 
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
