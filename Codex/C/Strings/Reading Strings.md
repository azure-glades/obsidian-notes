v[[Strings]]
There are 3 techniques to read strings
1. **scanf()**
```C
char str[20];
scanf("%s", str);
//unless 
scanf("%[^\n]s", str);
scantf("%[^\n]", str); //also works
//[] is called a scanset]
```
* Breaks when white-space is encountered -> Can only accept one word
* &str is not used because str is a local pointer for the string
* loop is not used since %s implies continuous character input
* To overcome this, scanset is used.
```c
scanf("%[abc]", str);
>>Here [abc] is called a scanset. Only a,b and c are accepted, and reading stops when any other character is encountered
>>It only scans the items in the set
>>using ^, [^abc] reading stops when a,b,c are encountered.
```

Input can also be suppressed (skipping certain inputs)
```c
scanf("%d%*c%d", &hour, &minute);
//any character between hour and minute is accepted and removed
>>Input: 9:15
>>hour = 9 and minute = 15. The ':' character is not read
```
When two scanf() statements are called, the remaining \\n from the previous input remains in the terminal (input stream) and gets take up by the next scanf(). To avoid this **fflush(stdin)** is used, or gets() can be used instead of scanf(). Furthermore, the `\n` can be ignored by adding the following
```c
scanf("%d%*c", &n);
//This takes the \n from the input stream and discards it
```

2. **gets()**: Simply accepts entire stirng including spaces.
 ```c
char str[50];
printf("Enter a string : ");
gets(str);
```
* Accepts complete string including whitespace
 3. **getchar():** Null character has to be manually assigned
 ```c
//Longer way
int i = 0;
while(ch != '\n')
 {
	ch = getchar();
	str[i]=ch;
	i++ 
 }
 str[i] = '\0' 
