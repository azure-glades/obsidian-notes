[[Files]]

1. **fprintf()**: fprint() works exactly like how printf() does, but it does printing to specific file-pointer instead of stdout.
```
SYNTAX: fprintf(FILE *, "input data %[type]", data);
```
```c
fprintf(fp, "lmao");
fprintf(stdout, "to terminal");
//prints to terminal
```
2. **fputs()**:  Puts string to a file
```
SYNTAX: fputs(char [], FILE *);
```
```c
char str[] = "stringerr";
fputs(str, fp);
```
3. **fputc()**
```
SYNTAX: fputc(char, FILE *);
```
```c
char ch = 'A';
fputc(ch, fp);
```
4. **fwrite()**:
```
SYNTAX: fwrite(array *, size-in-bytes, units-of-data, FILE *);
```
```c
char str[] = "this will be written";
fwrite(str, sizeof(char), strlen(str), fp);
```