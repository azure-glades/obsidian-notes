[[Structures]]

* structure variables can be assigned to other structure variables
* Cannot compare for equality (a1 == a2) is false
* Structures can be defined datatype like arrays.
	* Individual data members of a single value in array is called normally (a\[3].inter)
* Structure members can be arrays also
```c
struct complex{
	int real;
	int img;
}
```
* Structures can be initialized like arrays
```c
structure usrdata a = {2, 3}, b = {3, 4};
```
* Structures can be return types or arguments for a function
