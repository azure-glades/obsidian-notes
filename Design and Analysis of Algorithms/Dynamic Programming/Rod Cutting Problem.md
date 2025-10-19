Suppose you have a rod of length $n$, and you want to cut up the rod and sell the pieces in a way that maximizes the total amount of money you get. A piece of length $i$ is worth $p_i$ dollars

This problem is solved using [[Dynamic Programming]]. You only need 1 array to store optimized values in.

# Efficiency
Time complexity = $\Theta(n^2)$ 
Space complexity = $\Theta(n)$
Code
```c
#include <stdio.h>

// Function to find the maximum of two integers
int max(int a, int b) {
    return (a > b) ? a : b;
}

int bestCutting(int len, int val[]) {
	int dp[len+1];
	dp[0] = 0;
	//val[] is 1 indexing
	for(int i = 1; i < len+1; i++){
		int max_val = -1;
		for(int j = 1; j <=i ; j++){
			max_val = max(max_val, val[j] + dp[i-j]); 
		}
		dp[i] = max_val;
	}
	return dp[len];
}

int main() {
    int val[] = {0,1,4,3,5};
	int n = 4;
    printf("Maximum rod profit = %d\n", bestCutting(n,val));
    return 0;
}
```