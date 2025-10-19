To maximize the profit by fitting as many items as possible in a knapsack of maximum weight W, such that even fractional amount of items can be chosen

- Key premise: *profit-weight ratio* is used to identify the most optimal items
- Greedy choice is made where highest profit-weight items are continuously chosen until the max weight is reached


# Algorithm
```
FUNC frac_knapsack(int wt[], int val[], int n, int max)
//INPUT : weights, values, of n objects with knapsack capacity max
//OUTPUT : optimal choice of objects
	FOR(i<n,i:0->n)
		profit-by-wt[i] = val[i]/wt[i]
	FOR(i<n, i:0->n)
		k = getMax(pv,n)
		IF(max - wt[k] >= 0)
			max = max - wt[k]
			soln += val[k]
		ELSE
			ratio = max/wt[k]
			soln += ration*val[k]
			RETURN soln
		pv[k] = 0 //Eliminate repeat choice
RETURN soln
```

Code
```c
#include <stdio.h>
#include <stdlib.h>

// Function to find the maximum of two integers
int max(int a, int b) {
    return (a > b) ? a : b;
}

int getMax(float *pv, int n){
	float max = pv[0];
	int max_index = 0;
	for(int i = 1 ; i < n ; i ++){
		if(max < pv[i]){
			max = pv[i];
			max_index = i;
		}
	}
	return max_index;
}

int knapsack(int W, int wt[], int val[], int n) {
	float pv[n];
	float optim = 0;
	int maxin;

	for(int i = 0; i < n; i++){
		pv[i] = ((float)val[i])/((float)wt[i]);
	}	
	
	for(int i = 0; i < n; i++){
		maxin = getMax(pv,n);
		if(W - wt[maxin] >= 0 ){
			W = W - wt[maxin];
			optim += val[maxin];
		} else {
			float ratio = (float)W/(float)wt[maxin];
			optim 	+= (ratio*val[maxin]);
			return optim;
		}
		pv[maxin] = 0;
	}
	return optim;
}

int main() {
    int val[] = {1,2,5,6};
    int wt[] = {2,3,4,5};
    int W = 8;
    int n = sizeof(val) / sizeof(val[0]);

    printf("Maximum value in knapsack = %d\n", knapsack(W, wt, val, n));
    return 0;
}
```