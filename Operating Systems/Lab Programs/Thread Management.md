```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <math.h>
#include <pthread.h>

int a[4][4], b[4][4];

void* matrixEval(void* val){
	int *num = (int*)val;
	for(int i = 0; i<4; i++)
		b[(*num)][i] = a[(*num)][i];
	for(int i = 0; i<4; i++)
		for(int j = 0; j<(*num); j++)
			b[(*num)][i] *= a[(*num)][i] ;
}

int main()
{
	pthread_t tid[4]; int i, j;
	for(i = 0; i<4; i++)
	{
		printf("enter row elements %d: \n", i+1);
		for(j = 0; j<4; j++)
		{
		printf("\t");
		scanf("%d", &a[i][j]);
		}
	}
	printf("---input end---\n");
	for(i = 0; i<4; i++)
	{
		pthread_create(&tid[i], NULL, matrixEval,(void *)&i);
		sleep(1);
	}

	for(i = 0; i<4; i++)
		pthread_join(tid[i], NULL);
	printf("After processing: \n");
	for(i = 0; i<4; i++)
	{
		for(j = 0; j<4; j++)
		{
			printf("%d\t", b[i][j]);
		}
		printf("\n");
	}

	pthread_exit(NULL);
	return 0;
}
```


| Component                                   | Vendor                   | Cost (Including shipping) |
| ------------------------------------------- | ------------------------ | ------------------------- |
| RTL-SDR Blog V3 R860 RTL2832U 1PPM TCXQ SMA | RTL SDR Blog             | 3,000 INR                 |
| VBFZ-1400-S+                                | Mouser Electronics India | 6,300 INR                 |
| Nooelec SAWbird+ H1                         | Nooelec Inc.             | 5,000 INR                 |
|                                             | **Total**                | 14,300 INR                |
