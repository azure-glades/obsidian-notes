```c
#include <stdio.h>

int factorial(int);

int main()
{
	int n, result;
	printf("enter n🙂️: ");
	scanf("%d", &n);
	
	result = factorial(n);
	printf("\n%d\n", result);
	
	result = 1;
	for(int i = 0; i<n; i++)
	{
		printf("Iterating\t");
		result = result*(n-i);
	}
	printf("\n%d\n", result);
}

int factorial(int n)
{
	printf("Recursing\t");
	if(n==1)
		return 1;
	else
		return n*factorial(n-1);
}
```
