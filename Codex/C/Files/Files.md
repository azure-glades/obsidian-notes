[[Nexus ~ C]]
To use files:
1. Declare a file pointer variable
```c
FILE *fp ; //FILE is a structure in C
```
2. Open file on read/write mode
```c
fp = fopen("/home/azureglades/documents/cprog/file.txt", r);
```
* Here, **fopen()** is used to open and and assign a pointer to a file
```c
FILE fopen("path of file", mode);
```
file read/write modes.
![[Pasted image 20240730205838.png]]
* NULL pointer is returned if
	* File does not exist at path
	* File is open in another program
	* File access is not authorized
	* When it is an incompatible type

3. Close the file and free the pointer
	* Detaches the pointer from the file
	* Clears/flushes the input stream
	* Does **not** free the pointer. `free(fp);` has to be called separately
	* Program autocloses any file when terminated
```c
int fclose(FILE *fp);
//returns 0 if successful
int fcloseall();
//closes all pointers
```

* Inputs to program occurs via a file `stdin` that takes continuous input from the user and stores it as a stream of characters in `stdin`. 
* Similarly, output of program is written onto `stdout` which displays the stream of characters in the terminal
The characters stored in `stdin` or `stdout` file-pointer (called a ==file buffer==) can be cleared using 
```c
fflush(stdin); fflush(stdout);
flushall();
```

### Detecting EOF
```c
  if(fp == EOF)
	return;

if(feof(fp) == 0)
	return;
```
```
SYNTAX: int feof(FILE *)
>if EOF is reached, returns 0
>if EOF is not reached, returns 1
```