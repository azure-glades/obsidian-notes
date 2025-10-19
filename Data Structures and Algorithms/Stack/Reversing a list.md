```c
#include <stdio.h>
#define MAX 32

int stack[MAX];
int top = -1;

void pop();
void push(int);
void peek();

void main()
{
	int i, a, size;
	printf("Size: ");
	scanf("%d", &size);
	printf("Numbers:\n");
	for(i = 0; i<size; i++)
	{
		scanf("%d", &a);
		push(a);
	}
	
	printf("\nReversed: ");
	for(i = 0; i<size; i++)
	{
		peek();
		pop();
	}
	printf("\n");
}

void push(int n)
{
	stack[++top] = n;
}

void pop()
{
	stack[top--] = 0;
}

void peek()
{
	printf("%d ", stack[top]);
}
```
