*Definition:* An algorithm is a sequence of unambiguous instructions for solving a problem

>*Some problem types*
>Sorting
>Searching
>String processing
>Graph problems
>Combinatorics problems
>Geometric problems
>Numerical problems

> *Common strategies*
> Divide and Conquer
> Dynamic Programming

>*See further*
>[[Complexity Analysis]]
## Properties of algorithm
An algorithm is a sequence of unambiguous instructions for solving a problem. Key properties include:
1. **Input**: Valid inputs are specified. This ensures that the algorithm can process the data correctly.
2. **Output**: Expected outputs and their types are specified. This guarantees that the algorithm produces the desired result. 
3. **Finiteness**: The number of steps and execution time must be finite. All algorithms must terminate.
4. **Definiteness**: Each statement is clear and unambiguous. This ensures that the algorithm can be executed without confusion.
5. **Effectiveness**: It should solve the problem in as simple a manner as possible. This optimizes the algorithm's performance.

## Criteria
1. **Time** → Time taken to complete the task
2. **Space** → Memory taken to complete the task
3. **Network usage** → Data transfer done  to complete the task
4. **Power consumption** → Important for embedded system
5. **CPU Register usage** → Important when making kernel-level algorithms
Performance of algorithms is described using [[DAA 2]]
## Fundamentals of algorithmic problem solving
![[Pasted image 20250306211050.png]]


#### Example: **Algorithm to find GCD of two numbers**
1. **Euclids Algorithm:** This algorithm iteratively replaces `a` and `b` with `b` and the remainder of `a` divided by `b`, respectively, until `b` becomes zero. At that point, `a` is the GCD.
```algorithm
FUNCTION euclid(a, b)
//Input: numbers a and b
//Output: gcd of a,b
	WHILE b != 0
		r <- a mod b
		a <- b
		b <- r
	RETURN a
```

2. **Consecutive Integer Checking Method (CICM) Algorithm**: This method starts from the smaller of the two numbers and checks each integer to see if it divides both numbers evenly. The first such integer is the GCD.
``` algorithm
FUNCTION cicm(a, b)
	t <- min(a,b)
	WHILE t!=0
		IF (a%t == 0 AND b%t == 0)
			RETURN t
		t--
```

3. **Middle-school procedure:** By identifying the common prime factors of `a` and `b`, we can calculate their product to find the GCD.
```algorithm
FUNCTION gcd(a, b)
	>>primeFactors(a)
	>>primeFactors(b)
	>>Identify common prime factors
	>>Compute product of common factors
```

» **Sieve of Erathosthenes**
```algorithm
FUNCTION sieve(n)
//Implements sieve of erathosthenes
//Input: number n
//Output: primes less than n
	
```

