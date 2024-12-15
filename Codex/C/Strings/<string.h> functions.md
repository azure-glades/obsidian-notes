[[Reading Strings]]
[[Printing Strings]]
1. **strlen()**: length of string
```c
str = "abcdef";
strlen(str);
//Returns 5. '\0' is not counted
```
  2. **sizeof()**: String length, includes \\0 also. Sizeof() works on array also
```c
char x[10] = "abcd";
strlen(x);
// returns 4 as int
sizeof(x);
//returns 5 as int
```
3. **strcpy()**: copy string
```c
char x[5] = "abcd", y[5];
strcpy(y,x);
//x is copied to y
```
4. **strcat()**: concatenates 2 strings and stores it in first string
```c
char x[20] = "cats ", y[5] = "dogs"
strcat(x,y);
// x = "cats dogs"
// y = "dogs"
```
5. **strcpy()**: Copies string 2 to string 1. 
6. **strncpy()** : Copies string 2 to 1, specify no of characters to be copied. \\0 has to be assigned to terminate, else older values continue
```c
char x[20] = "cats ", y[10] = "dogs";
strcpy(x,y) ;
// y is copied to x
strncpy(x,y,3) ;
x[3] = '\0';
// x is dog. if \0 is not used, x is dogs, where s is the last character in cat's'
```
7. **strstr():** Used to locate strings
8. **strchr()**:Used to locate from front
9. **strrchr()**:Used to locate character from back.
	returns int value of position
```c
char x[] = "abcdefghijk";
strstr(x, "efg"); //returns 4 (since x[4] is where it starts)
strchr(x, 'd'); //returns 3 (since x[3] = d)
strrchr(x, 'd'); //returns
```
11. **strcmp()**: Returns 0 if strings are equal
			if str1 > str2 : positive
			if str1 < str2 : negative
```c
char x[10] = "abcd", y[10] = "abcd", z[10] = "abc";
printf("%d, %d, %d", strcmp(x,y), strcmp(x,z));
//output is 0, -1.
```
12. **strrev():** Reverses the string
13. **strlwr()**: Converts string to lower case
14. **strupr()**: Converts string to upper case