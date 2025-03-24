→ do time complexity analysis on matrix mul, distinct array and decimal to binary
## Mathematical time complexity analysis
- Forward and backward substitution
- Recursive Tree
- Masters theorem

```algorithm
FUNCTION factorial(n)
	IF n = 0
		RETURN 1
	ELSE
		RETURN n*factorial(n)   // basic operation *
```

Base condition : `n = 0`
Steps taken for `f(n)`: `f(n-1) + 1` steps → This is a recurrence relation
→ solve for factorial and tower of hanoi

Section 4 in intro to algos. fwd and bkd substitution, recursion tree, master theorem, akra bazzi recurrence
