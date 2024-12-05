***Recursive function is a function that calls itself***
- Tail recursion: Recursive call is after applying logic
- Head recursion: Recursive call is before applying logic
Recursion is *top-down approach* to problem solving since it divides it into smaller sub problems and solves each of those sub problems by dividing them further, until it reaches the smallest base case where logic is applied 

Iteration is *bottom-up approach* where solving begins with what is known and is and builds up the main solution with that

> EX: [[Factorial Function]]
```algorithm
int factorial(n)
{
	if(n == 1) return 1
	return n*factorial(n-1)
}

print(factorial(n))
```

``` algorithm
result = 1
for(int i = 0; i<n; i++)
{
	result = result*(n-i)
}
print(result)
```

>EX: [[Fibonacci Function]]
```algorithm
int fibonacci(n)
{
	if(n == 1) return 1;
	if(n == 0) return 0;
	printf(n);
	return fibonacci(n-1) + fibonacci(n-2);
}
```

```algorithm
fib[0] = 0;
fib[1] = 1;
for(int i = 2; i<=n; i++)
{
	fib[i] = fib[i-1]+fib[i-2];
}

print(fib[n])
```
>EX: [[Tower of Hanoi]]
>EX: [[Binary Search]]

Function calls are stored in **call stack**. Call stack stores the functions that are called in sequence. first in first out.
- When a function calls another function, the master function remains paused and waits until the slave function finishes.
- In recursion, the 1st recursive call is paused and waits until the recursive calls under it complete execution, which also have to wait until all recursive calls under them finish execution too

Rercursion is usually slower than iterations because of repeated function calls needing to have memory allocated, while iterations use loops.
