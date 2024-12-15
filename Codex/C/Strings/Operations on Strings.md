[[<string.h> functions]]

Characters of a string are stored as ASCII values, which can be modified with operators

```C
char x = 'a';
printf("%d", x); //displays the ASCII value
printf("%c", x+1); //displays next character : b
```

ASCII for A-Z : **65 to 91**
ASCII for a-z: **97 to 123**
		+- 32 converts between the cases
		26 characters in the alphabet
