**Dangling pointer** is a pointer that doesnt point to an object of appropriate type. They are pointers that point to invalid memory locations. Dereferencing a dangling pointer causes *undefined behaviour*.
- Ex:
```c
#include <stdlib.h>

void func()
{
    char *dp = malloc(A_CONST);
    /* ... */
    free(dp);         /* dp now becomes a dangling pointer */
    dp = NULL;        /* dp is no longer dangling */
    /* ... */
}
```
```c
int *func(void)
{
    int num = 1234;
    /* ... */
    return &num; //num is a stack variable, the value is not stored and merely points to the location it was once stored
}
```
```c
{
   char *dp = NULL;
   /* ... */
   {
       char c;
       dp = &c;
   } 
     /* c falls out of scope */
     /* dp is now a dangling pointer */
}
```

**Wild pointers** are uninitialized pointers.
```c
int f(int i)
{
    char *dp;    /* dp is a wild pointer */
    static char *scp;  
    /* scp is not a wild pointer:
    * static variables are initialized to 0
    * at start and retain their values from
    * the last call afterwards.
    * Using this feature may be considered bad
    * style if not commented */
}
```

**Null pointers** are pointers that are initialized to the `NULL` value. `NULL` does not point to a location and hence, dereferencing a null pointer throws an error in C. To prevent dangling pointers, all deallocated pointers are set to `NULL`.

**Void pointers** are pointers that dont have a specific data-type and can be type-casted to pointers of any other type. They are **Generic pointers**
