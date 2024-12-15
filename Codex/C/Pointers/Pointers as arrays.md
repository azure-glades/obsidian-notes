[[Pointers]]

Pointers can be used as indices for arrays beginning at custom location of an array
```c
main(){
	int a[] = { 1,2,3,4,5};
	int *p;
	p = &a[1]; //*p stores a[1] = 2
	p++; //*p points to a[2] now
	*p++; //a[2] has increased by 1 (a[2] = 4)
}
```
i.e Pointers can be used to dynamically refer to arrays;
```
a[0] : p - 2
a[1] : p - 1
a[2] : p = &a[2] 
a[3] : p + 1
a[4] : p + 2
a[5] : p + 3

suppose p++
then
a[0] : p - 3
a[1] : p - 2
a[2] : p - 1
a[3] : p = &a[3]
a[4] : p + 1
a[5] : p + 2
```