[[Functions]]
* **Call by Value**: Function makes copy of input data
```c
int times10(int n){
	n *= 10;
	return n;
}
```
* **Call by Reference:** References actual input variable and makes changes to it. uses variable address as input
```c
int mult10(int *p){
	*p *= 10 ;
	return *p ;
}
```
Controls output
```c
main(){
	int n = 20;
	int m = 20;
	int *p = &m;
	times10(n);
	mult10(p);
	printf("%d\n%d\n", n, m);
}
//also can be called as
mult10(&m);
//pointer need not be used, address can be used
```
>>n = 20
>>m = 200

Function modifies data at the address stored by pointer.