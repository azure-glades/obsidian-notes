
Stack / Primitive functions of stack
Primitive, linear ds
first in last out
>Bracket matching program


### Infix-Postfix-Prefix
Method of defining operators
- infix : a+b
- postfix: ab+
- prefix: +ab

>EX: a+b\*c
>Convert to postfix: a+bc\* -> (a(bc)\*)+ -> abc*+ 
>Convert to prefix: a + (\*bc) -> +a(\*bc) -> +a\*bc

> Convert [[Infix to Postfix]]
>Write an algorithm using stack to do [[Postfix Evaluation]]
```algorithm
s = empty-stack

while(!end-of-expression)
{
	symbol = next-character-from-expression
	if(symbol != operator)
	{
		push(s, symbol)
	}
	else
	{
		operand2 = pop(s)
		operand1 = pop(s)
		result = operation(operand1, operand2)
		push(result)
	}
}

return pop(s)
```

> *(10 mk)* Evaluate the given expression using stack with a trace: 6 2 3 + - 3 8 2 / + \* 2 $ 3 +

| symbol | operand2 | operand1 | result | stack-trace |
| ------ | -------- | -------- | ------ | ----------- |
| 6      |          |          |        | 6           |
| 2      |          |          |        | 6, 2        |
| 3      |          |          |        | 6, 2, 3     |
| +      | 3        | 2        | 5      | 6, 5        |
| -      | 5        | 6        | 1      | 1           |
| 3      |          |          |        | 1, 3        |
| 8      |          |          |        | 1, 3, 8     |
| 2      |          |          |        | 1, 3, 8, 2  |
| /      | 2        | 8        | 4      | 1, 3, 4     |
| +      | 4        | 3        | 7      | 1, 7        |
| *      | 7        | 1        | 7      | 7           |
| 2      |          |          |        | 7, 2        |
| $      | 2        | 7        | 49     | 49          |
| 3      |          |          |        | 49, 3       |
| +      | 49       | 3        | 52     | **52**      |
> Convert [[Infix to Prefix]]
> Write an algorithm using stack to do [[Prefix Evaluation]]
```algorithm
s = empty-stack
expression2 = reverse-expression1

while(!end-of-expression2)
{
	symbol = next-character-from-expression2
	if(symbol != operator)
	{
		push(s, symbol)
	}
	else
	{
		operand1 = pop(s)
		operand2 = pop(s)
		result = operation(operand1, operand2)
		push(result)
	}
}

return pop(s)
```

> *(10 mk)* Evaluate the given expression using stack with a trace: - +  5 \* 6 2 1

reversed expression: 1 2 6 * 5 + -

| symbol | operator2 | operator1 | result | stack-trace |
| ------ | --------- | --------- | ------ | ----------- |
| 1      |           |           |        | 1           |
| 2      |           |           |        | 1, 2        |
| 6      |           |           |        | 1, 2, 6     |
| *      | 6         | 2         | 12     | 1, 12       |
| 5      |           |           |        | 1, 12, 5    |
| +      | 5         | 12        | 17     | 1, 17       |
| -      | 17        | 1         | 16     | **16**      |
