```c
#include <stdio.h>
#define MAX 64

int fibonacci(int);

int main()
{
	int fib[MAX] , n;
	printf("enter n: ");
	scanf("%d", &n);
	
	fib[0] = 0;
	fib[1] = 1;
	for(int i = 2; i<=n; i++)
	{
		fib[i] = fib[i-1]+fib[i-2];
	}
	
	printf("iterative %dth Fibonacci: %d\n\n", n, fib[n]);
	
	int result = fibonacci(n);
	printf("recursive %dth Fibonacci: %d\n", n, result);
	return 0;
}

int fibonacci(int n)
{
	printf("%d\n", n);
	if(n == 1) return 1;
	if(n == 0) return 0;
	return fibonacci(n-1) + fibonacci(n-2);
}
```
