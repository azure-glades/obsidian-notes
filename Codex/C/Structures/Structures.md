[[Nexus ~ C]]

structure is essentially a user defined data type
tag is name of structure
structure has data members

* structures are referred as
```c
struct tag (function/call/variable name)
```
multiple variables can be declared from structure. Either after structure definition or in main as 
```c
main()
{structure tag var1, var2, var[];}

structure tag{data members} var1, var2, var3[];
```

data members are accessed using '.'
```c
var1.i;
var1.ch;
var[3].ch;
```
EX: used for complex calculator: new complex data type