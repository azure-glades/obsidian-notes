[[Operators]]
Simple assignment: Storing value
Compound assignment: updating value
* right to left always --> right associative
``` c
i = e ;
//i is called 'lvalue' = 'left value'
// i always recieves value of e. e is always converted to the type of i
```
Right associative
``` c
i=j=k=0 
// means i=(j=(k=0))
```
Can cause **side effects**
``` c
int i
float f
f = i = 33.33 ;
//i = 33
//f = 33.00000 not 33.33
//data is lost
```
Compound Assignment : +=, -=, *= , /=. %=
``` c
i+=2; //is i = i + 2
i %= 10 ; //is i=i%10

//but 
i*= j+k; //is not i = i*j+k, it is i = i*(j+k)

```