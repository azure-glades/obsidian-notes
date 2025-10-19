## Flowchart
![[Pasted image 20241016200259.png]]
> Write a c program with recursive functions to solve tower of hanoi problem
```c
#include <stdio.h>
#define MAX 32

void towerofhanoi(int, char, char, char);
int count = 1;
void main()
{
	int n;
	printf("Enter the number of disks: ");
	scanf("%d", &n);
	towerofhanoi(n, 'a', 'b', 'c');
	printf("\nNumber of moves %d\n", count);
}

void towerofhanoi(int n, char src, char aux, char dest)
{
	if(n == 1)
	{
		printf("\n Move %d from %c to %c\n", n, src, dest);
		count++;
		return;
	}
	towerofhanoi(n-1, src, dest, aux);
	printf("\nMove %d from %c to %c\n", n, src, dest);
	count++;
	towerofhanoi(n-1, aux, src, dest);`
}
```
