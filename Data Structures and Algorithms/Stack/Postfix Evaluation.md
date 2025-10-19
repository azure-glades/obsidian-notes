```c
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>
#include <math.h>
#include <string.h>
#define SIZE 32

// Stack structure for floats
struct stack{
	int top;
	float a[SIZE];
};

void push(struct stack *s, float n);
float pop(struct stack *s);
float operate(float op1, float op2, char symbol);
float evaluate_postfix(struct stack *s, char postfix[]);

int main() {
	char postfix[SIZE];
	struct stack s;
	s.top = -1;
	float answer;

	printf("Postfix: ");
	scanf("%s", postfix);
	answer = evaluate_postfix(&s, postfix);
	printf("\nAnswer: %.0f\n", answer);
	return 0;
}

void push(struct stack *s, float n) {
	s->a[++(s->top)] = n;
}

float pop(struct stack *s) {
	return s->a[(s->top)--];
}

float operate(float op1, float op2, char symbol) {
	switch(symbol) {
		case '+': return op1 + op2;
		case '-': return op1 - op2;
		case '*': return op1 * op2;
		case '/': return op1 / op2;
		case '^': return pow(op1, op2);
		default: return 0;
	}
}

float evaluate_postfix(struct stack *s, char postfix[]) {
	int i;
	char symbol;
	float op1, op2;

	// Process each character in the postfix expression
	for(i = 0; i < strlen(postfix); i++) {
		symbol = postfix[i];

		if(isdigit(symbol)) {
			// Convert character to float and push to stack
			push(s, symbol - '0');
		} else {
			// Pop two operands from the stack for the operation
			op2 = pop(s);
			op1 = pop(s);
			// Perform the operation and push the result back to the stack
			push(s, operate(op1, op2, symbol));
		}
	}

	// The final result is the last remaining element in the stack
	return pop(s);
}
```