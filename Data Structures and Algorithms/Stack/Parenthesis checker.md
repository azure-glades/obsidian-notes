Checks if all opened brackets are closed correctly
```c
#include <stdio.h>
#define MAX 32

char stack[MAX];
int top = -1;

void pop();
void push(char);
char peek();
int isempty();

void main()
{
	int i, size;
	char a, dum;
	printf("Size: ");
	scanf("%d", &size);
	printf("Brackets: ");
	scanf("%c",&dum);
	for(i = 0; i<size; i++)
	{
		scanf("%c", &a);
		if(a == '(' || a == '{' || a =='[' || a=='<')
			push(a);
		else
			switch(a)
			{
				case ')':
					if(peek() == '(')
						pop();
					break;
				case '}':
					if(peek() == '{')
						pop();
					break;
				case ']':
					if(peek() == '[')
						pop();
					break;
				case '>':
					if(peek() == '<')
						pop();
					break;
				default:
					//printf("\nWRONG\n");
					break;
			};
	}
	if(isempty() == 1)
		printf("\nCORRECT\n");
	else
		printf("\nWRONG\n");
}

void push(char n)
{
	stack[++top] = n;
}

void pop()
{
	stack[top--] = 0;
}

char peek()
{
	printf("%c ", stack[top]);
	return stack[top];
}

int isempty()
{
	if(top == -1)
		return 1;
	else
		return 0;
}
```