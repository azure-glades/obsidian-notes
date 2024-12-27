### Evaluating infix to postfix
Bodmas is followed
- (a+b)\*c -> (ab+)\*c -> (ab+)c\* -> ab+c\*
- a+b\*c -> a+(bc\*) -> a(bc\*)+ -> abc\*+
- a+b-c\*d+e -> a+b-(cd\*)+e -> (ab+)-(cd\*e+) -> (a+(b(cd\*e+)-) -> a(bcd\*e+-)+ -> abcd\*e+-+
- a+b-c -> a+bc- -> abc-+
- a+b\* c -> a+bc\* -> abc\*+
- a\*b+c -> (ab*) + c -> c(ab*)+

> Convert a valid infix expression without parenthesis into postfix expression:
```algorithm
s = empty-stack

while(!end-of-expression)
{
	symbol = next-char-from-expression
	if(symbol == operator)
	{
		if( top == NULL )
		{
			push(symbol)
		}
		if(top(s) <= symbol)
		{
			push(symbol)
		}
		else
		{
			print(top(s))
			pop()
			push(symbol)
		}
	}
	if(symbol == operand)
	{
		print(symbol)
	}
}

print()
```

```c
#include <stdio.h>
#include <ctype.h>
#include <stdlib.h>
#include "char_stack.h"
#define SIZE 32
int precedence(struct stack*, char);
void toPostfix(struct stack *, char []);
void main()
{
	struct stack s;
	s.top = -1;
	char infix[SIZE];
	printf("Infix expression: ");
	scanf("%s", infix);
	toPostfix(&s, infix);
	return;
}

int preced(char symbol)
{
	switch(symbol)
	{
		case '+':
		case '-':
			return 1;
		case '*':
		case '/':
			return 3;
		case '^':
			return 5;
	}
}

void toPostfix(struct stack *s, char infix[SIZE])
{
	int i, j = 0;
	char postfix[SIZE], temp, symbol;
	for(i = 0; infix[i] !='\0'; i++)
	{
		symbol = infix[i];
		if(isalnum(symbol))
		{
			postfix[j++] = symbol;
		}
		else
		{
			switch(symbol)
			{
				case '(':
					push(s, symbol);
					break;
				case ')':
					temp = pop(s);
					while(temp != '(')
					{
						postfix[j++] = temp;
						temp = pop(s);
					}
					break;
				case '+':
				case '-':
				case '*':
				case '/':
				case '^':
					if(s->top == -1 || s->a[s->top]=='(')
					{
						push(s, symbol);
					}
					else
					{
						while(preced(s->a[s->top])>=preced(symbol) && s->top != -1 && s->a[s->top] != '('){
							postfix[j++] = pop(s);
						}
						push(s, symbol);
					}
					break;
				default:
					printf(" Invalid expression error\n");
					exit(0);
			}
		}
	}
	while(s->top != -1)
		postfix[j++] = pop(s);
	postfix[j] = '\0';
	printf("Expression: %s\n", postfix);

}








```