[[Structures]]

**typedef()** lets you set alternate names for primitive and use-defined data types. creates a name for existing data. Alias
```c
/*syntax*/ typedef <tag> <alias> ;
typedef struct nums{
	float real;
	float img;
} complex ;

/*or*/ typedef struct nums complex;

typedef int NUM; //int can be refered as NUM

//here comp is the new name
complex a, b ;
struct nums a, b;
```
* Aliases can be used as return types and arguments for functions
```c
void swap (complex x, complex y)
{
	complex temp;
	x.real = temp.real ;
	x.real = y.real;
	y.real = temp.real;

	x.img = temp.img ;
	x.img = y.imp ;
	y.img = temp.img ;
}

complex conjugate(complex x)
{
	complex t ;
	t.real = x.real;
	t.img = -x.img ;
	return t ;
}
```