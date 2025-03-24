```c
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>
#include <math.h>
#include <string.h>
#define SIZE 32

//float stacks
struct stack{
	int top;
	float a[SIZE];
};

void push(struct stack *, float);
float pop(struct stack *);
float operate(float, float, char);
float evaluate(struct stack *, char []);

void main(){
	char prefix[SIZE];
	struct stack s;
	s.top = -1;
	float answer;

	printf("Prefix: ");
	scanf("%s", prefix);
	answer=evaluate(&s, prefix);
	printf("\nAnswer: %.0f\n", answer);
}

void push(struct stack *s, float n){
	s->a[++(s->top)] = n;
}

float pop(struct stack *s){
	return s->a[(s->top)--];
}

float operate(float op1, float op2, char symbol){
	switch(symbol){
		case '+': return op1+op2;
		case '-': return op1-op2;
		case '*': return op1*op2;
		case '/': return op1/op2;
		case '^': return pow(op1, op2);
	}
}

float evaluate(struct stack *s, char prefix[SIZE]){
	int i;
	char symbol;
	float res, op1, op2;
	for(i = strlen(prefix)-1; i>=0; i--){
		symbol = prefix[i];
		if(isdigit(symbol))
			push(s, symbol - '0');
		else{
			op1 = pop(s);
			op2 = pop(s);
			float result = operate(op1, op2, symbol);
			push(s, result);
		}
	}
	return pop(s);
}
```