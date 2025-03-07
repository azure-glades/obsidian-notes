

```c
#include <stdio.h>
#define MAX 32

int binsrh(int, int, int);
int a[MAX];

int main()
{
	int size, search;
	printf("Size? ");
	scanf("%d", &size);
	
	for(int i = 0; i<size; i++)
	{
		printf("\nElement %d: ", i);
		scanf("%d", &a[i]);
	}

	printf("Search element: ");
	scanf("%d", &search);
	int position = binsrh(0, size, search);
	if(position == -1)
		printf("Search NULL\n");
	else
		printf("Found at %d\n", position);


	return 0;
}

int binsrh(int bottom, int top, int element)
{

	if(a[bottom] == element)
		return bottom;
	else if(a[top] == element)
		return top;

	int mid = (top+bottom)/2;

	if(mid == bottom || mid == top)
		return -1;
	if(a[mid] == element)
		return mid;
	else if(a[mid]<element)
		return binsrh(mid, top, element);
	else if(a[mid]>element)
		return binsrh(bottom, mid, element);
}
	