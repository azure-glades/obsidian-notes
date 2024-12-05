***Allocation of memory at run-time***
Implemented via c standard functions

### `malloc()`: Memory Allocate
Reserves a block of memory for the specific number of bytes.
Returns a void pointer which is type-caste to other data-types.
```
ptr = (cast-type*)malloc(size-in-bytes)
```
Ex:
```c
fptr = (float*)malloc(10*sizeof(float));
cptr = (char*)malloc(10);
```
- Does not remove garbage values that were previously stored in the location
- Returns `NULL` if allocation fails

### `calloc()`: Continuous Allocate
Reserves a block of contiguous memory
```
ptr = (cast-type)calloc(n, size)
```
Ex:
```c
fptr = (float*)calloc(25, sizeof(float));
```
- Wipes the garbage values that were previously stored in location
- Returns `NULL` if allocation fails

### `realloc()`: Re allocate
Changes the size of allocated memory block to the new size
Accepts a pointer that has already been allocated memory
```
ptr = realloc(ptr, n)
```
Ex:
```c
ptr = realloc(ptr, 200);
```
- if the existing space cannot be extended, then a new block of contiguous memory is allocated and the data is completely transferred to the new location
- Returns `NULL` if reallocation fails and releases the original memory blocks - Original memory is completely lost

### `free()`: Frees memory
Assigned memory is freed.
```c
free(ptr);
```

### Dangling Pointer
Dangling pointer is a pointer pointing to a memory location that has been freed
- Function call
- De-allocation of memory
- Out of scope variable

***Memory leaks***
***Null pointers***
***Void pointers***
