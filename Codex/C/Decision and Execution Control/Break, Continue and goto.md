[[Loops or Iterative Statements]]
* **Break** exits the loop completely
* **Continue** Skips 1 iteration of the loop
* **goto** Skips to another part of program
```c
for(i = 0; i<10; i++)
{
	if(i == 5)
		 break;
	printf("%d\n", i);
} //prints till 4

for(i = 0; i<10; i++)
{
	if(i == 5)
		 continue;
	printf("%d\n", i);
} //prints 0 to 9 but skips 5
```
goto is generally not used.
```c
label:
	//code
goto label;
>> Backward jump since goto is pointing to previous line of code. code is executed multiple times.

goto label;
	//code1
label:
	//code2
>> Forward jump. code1 is not executed
```
