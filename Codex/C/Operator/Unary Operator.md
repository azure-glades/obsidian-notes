[[Operators]]
* Pre-Increment: (++i)
	Value of i is changed before evaluating expression.
* Post-Increment: (i++) 
	Value of i is changed after evaluating expression

```
int x, a = 10, b = 20;
x = 50+ ++a ; //x is 61, a = 11. 
x = 50+ a++; //x is 60, a = 11
x = a++ + b++; //x = 30, a = 11, b = 21

x = ++a - ++a; //x = 0, a = 12. both the ++a is evaluated first, then x value is assigned
x = ++a - a++; //x = 1, a = 12. a++ is evaluated. x value is assigned, a++ is evaluated
x = a++ - ++a //x = -2, a= 12. for the expression a++ = 10. therefore x = 10 - a++. Here a now becomes 11 (since a++ is evaluated but not used in expression). then ++a is 12. x = 10 - 12

int n = 1, m;
m = n++ + n++ // m = 6. Both n++ are evaluated first so n =3. m = 3+3
m = ++n + ++n // m = 3. n++ is evaluated. Since another ++n has to be evaluated
```