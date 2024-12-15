[[Nexus ~ C]]
	Not a datatype: Array of characters
* strings are stored at memory locations, called by pointers
* strings terminate with a null character: '\\0'
* strings are stored on char\[]  with  getString() function.
* declared using char s\[] or char \*p  (as pointer)
* Format specifier: **%s**


Declaring strings:
```C
char c[] = "abcd";
char c[5]="abcd";
//Or using pointers
char *c = "abcd";
char c[]={'a','b','c','d','\0'};
//Null character has to be defined
char c[] = {'a', 'b', 'c', 'd'}; >>Considered a string but doesnt terminate.
//
char str[];
str = "abcd"; >>Throws an error
//
char str[3]= "abcd" >>Throws an error
//
```

C permits empty string ("") but doesnt permit empty character
![[Pasted image 20240718225634.png]]
![[Pasted image 20240718225735.png]]
When extra characters are left empty
