> Convert a valid infix expression without parenthesis into prefix expression:
```algorithm


```
**C program:**
```c
#include <stdio.h>
#include <ctype.h>
#include <string.h>
#include "char_stack.h"  // Make sure this contains `push` and `pop` functions
#define SIZE 32

int precedence(char symbol);
void infixToPrefix(struct stack *s, char infix[], char prefix[]);

int main() {
    struct stack s;
    s.top = -1;
    char infix[SIZE], prefix[SIZE];

    printf("Infix expression: ");
    scanf("%s", infix);

    infixToPrefix(&s, infix, prefix);
    printf("Prefix Expression: %s\n", prefix);

    return 0;
}

int precedence(char symbol) {
    switch (symbol) {
        case '+':
        case '-':
            return 1;
        case '*':
        case '/':
            return 3;
        case '^':
            return 5;
        default:
            return 0;
    }
}

void reverseString(char str[]) {
    int length = strlen(str);
    for (int i = 0; i < length / 2; i++) {
        char temp = str[i];
        str[i] = str[length - i - 1];
        str[length - i - 1] = temp;
    }
}

void infixToPrefix(struct stack *s, char infix[], char prefix[]) {
    // Step 1: Reverse the infix expression
   reverseString(infix);

    // Step 2: Replace '(' with ')' and vice versa
    for (int i = 0; infix[i] != '\0'; i++) {
        if (infix[i] == '(')
            infix[i] = ')';
        else if (infix[i] == ')')
            infix[i] = '(';
    }

    // Step 3: Convert the modified infix expression to postfix
    int j = 0;
    char symbol;
    char tempPostfix[SIZE];

    for (int i = 0; infix[i] != '\0'; i++) {
        symbol = infix[i];

        if (isalnum(symbol)) {
            tempPostfix[j++] = symbol;
        } else {
            switch (symbol) {
                case '(':
                    push(s, symbol);
                    break;
                case ')':
                    while (s->top != -1 && s->a[s->top] != '(') {
                        tempPostfix[j++] = pop(s);
                    }
                    pop(s);  // Remove '(' from stack
                    break;
                case '+':
                case '-':
                case '*':
                case '/':
                case '^':
                    while (s->top != -1 && precedence(s->a[s->top]) >= precedence(symbol)) {
                        tempPostfix[j++] = pop(s);
                    }
                    push(s, symbol);
                    break;
            }
        }
    }

    // Pop remaining operators from the stack
    while (s->top != -1) {
        tempPostfix[j++] = pop(s);
    }
    tempPostfix[j] = '\0';

    // Step 4: Reverse the postfix expression to get prefix
    reverseString(tempPostfix);
    strcpy(prefix, tempPostfix);
}


```