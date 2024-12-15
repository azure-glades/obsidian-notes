[[Computer Memory]]
* Creation
```c
int *ptr1 ;
int *ptr2 ;
```
* Dereference
* Indirect assignment
* Assignment
```c
int i = 1;
int j = 200;

ptr1 = &i ; //i1 has been moved to ptr1 location
ptr2 = ptr1; /* throws an error */

ptr1 = j ;
//i value becomes 200
```