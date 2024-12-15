[[Decision Control]]

* *while*  and *do-while*  are indefinite loops since number of iterations is not known. 
	* Also called Sentinel control loops since their execution depends on a sentinel/checking condition
	* **do-while** is called ==bottom-checking loop/exit controlled loop/post-test loop== since condition is checked after execution of code-block
	* **while** is called ==top-checking loop/entry controlled loop/pre-test loop== since condition is checked before execution of code-block
* *For*  is definite loops since number of iterations is known
	* Also called counter control loops since a counter  with condition is used to control the execution of code
Nested loops of these combinations are allowed
```c
while(cond)
{
	//statements
}

do
{
	//statements
} while(cond)

for(initialize var; condition; variable update)
{
	//statements
}
```
All 3 parameters for for-loop need not be used
```c
int i = 0;
for(;i<=64;i++) //(i<=64; i++) is wrong
{
	printf("%d\n",i); //prints i to 64
}
for(;i<=64;) //(i<=64) is wrong
{
	printf("%d\n",i); //prints i to 64
	i++;
}

for(;;)
{
	printf("A\n");
} //will print A for ever.
```