[[Files]]

1. **fscanf()**: fscanf() works exactly like how scanf() does, but it does reading from specified file pointer instead of stdin. Multiple characters can be read.
```
SYNTAX: fscanf(FILE *, "%[input-specifies]", data-types);
```
```c
fscanf(fp, "%d %s %c", &rollno, name, &gender);
fscanf(stdin, "%d", &in);
//takes input from terminal
```
2. **fgets()**: Gets a string of characters of specified length and stores it in a string
```
SYNTAX: fgets(string-name, size int, FILE *);
```
```c
fgets(str, 8, fp);
//accepts 8 characters and stores into str.
//Accepts until it reaches '\n' or EOF
```
3. **fgetc()**: Gets the next character from file.
```
SYNTAX: fgetc(FILE *);
```
```c
char = fgetc(fp);
```
4. **fread()**
```
SYNTAX: fread(array*, size-in-bytes, units-of-data, FILE *);
```
```c
char str[32];
fread(str, sizeof(char), 32, fp);
```