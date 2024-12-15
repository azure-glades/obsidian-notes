[[Decision Control]]

Executes code block when condition is satisfied
```c
if(bool_condition)
{
	//statements;
}
>>0 : FALSE
>>NOT 0 : TRUE

if(1)
{
	//ALWAYS EXECUTED
}
if(0)
{
	//NEVER EXECUTED
}
```

When condition is not satisfied, another block of code can be optionally executed.
```c
if(bool_condition)
{
	//statements
}
else
{
	//statements
}
//{} need not be used
if(cond)
	statement;
else
	statement;
```

when multiple have to be checked, else-if is used
```c
if(bool_condition)
{
	//statements
}
else if(bool_condition#2)
{
	//statments
}
else
{
	//statments
}
```
nested ifs are called if-else ladders
```c
if(cond1)
{
	if(cond2)
	{
		if(cond3)
		{
			//statement
		}
	}
}
```
### Dangling else problem
When there is no matching *else*  case for every *if*  statement
```c
if(a>b)
	if(a>c)
		printf("a greater than b and c");
	else
		printf("a is not greater than b and c");
```
Here, else is always paired with the inner if statement. Brackets are used for more clarity.
```c
if(a>b)
	if(a>c)
	{
		printf("a greater than b and c");
	}
else
	printf("a is not greater than b and c");

```
Here, else is paired with outer if statement.