Driver code
```c
#include <stdio.h>
#include <string.h>
#include <sys/types.h>
#include <unistd.h>
#include <stdlib.h>
#include <wait.h>

int main(int argc, char *argv[])
{
	printf("\nmain function: ");
	int flag = 1;
	pid_t pid=fork();
	printf("%x", pid);

	if(pid < 0){
		printf("not forked\n");
	}
	else if(pid == 1){
		printf("\nChild PID: %x\nParent PID: %x\n", getpid(), getppid());
		execl("./binsrh", argv[1], NULL);
	} else {
		printf("\nParent PID: %x\n", getpid());
		printf("waiting ...\n\n");
		wait(&flag);
		if(WIFEXITED(flag) == 1)
		{
			printf("child killed normally...\n");
		} else {
			printf("child killed abnormally...\n");
			exit(0);
		}
	}

	printf("---eop---\n");
	return 0;
}
```

Child code
```c
#include <stdio.h>

int binarySearch(int arr[], int l, int r, int x)
{
	if(r>=1)
	{
		int mid = (r+l)/2;
		if(arr[mid] == x)
			return mid;
		if(arr[mid] > x)
			return binarySearch(arr, l, mid-1, x);
		else
			return binarySearch(arr, l, mid+1, x);
	}
	return -1;
}

void swap(int *xp, int *yp)
{
	int temp = *xp;
	*xp = *yp;
	*yp = temp;
}

void sort(int arr[], int n)
{
	int i, j;
	for(i = 0; i<n-1; i++)
		for(j=0; j<n-i-1; j++)
			if(arr[j]>arr[j+1])
				swap(&arr[j], &arr[j+1]);
}

int main(void)
{
	int n, key, arr[10];
	printf("Enter array size: ");
	scanf("%d", &n);
	printf("\nEnter array elements:\n");
	for(int i = 0; i<n; i++)
		scanf("%d", &arr[i]);
	sort(arr, n);
	printf("Search element: \n");
	scanf("%d", &key);
	int result = binarySearch(arr, 0, n-1, key);
	if(result == -1)
		printf("Element is absent");
	else
		printf("Element present at %d\n", result);
	return 0;
}
```

