[[Strings]]
1. **printf()**:  Prints a string using %s.
 ```c
char* str ="this is a string";
printf("%s", str);
printf("%3s", str);
>>Outputs "thi". specifies number of characters

char str[] = "abc"
printf("%5s%s", str, str);
>>Outputs "  abcabc". Ensures output has 5 characters or more. Pads empty space *before* string if smaller

printf("%-5s%s", str, str);
>>Outputs "abc  abc". nsures output has 5 characters or more. Pads empty space *after* string if smaller
```
2. **puts()**: Prints a string and terminates automatically with newline character
```c
char str[] = "abcd";
puts(str);
```
3. **putchar()**: Loops are used
```c
i = 0;
while(str[i] != '\n')
{
	putchar(str[i]);
	i++;
}
```
