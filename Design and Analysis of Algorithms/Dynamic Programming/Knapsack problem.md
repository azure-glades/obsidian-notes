A knapsack is a sack that can store a set capacity/weight of items
each item has its weight and value
problem is put items in the knapsack such that the total value is maximum staying under the knapsack capacity
It is an optimization problem, where we maximize the value function with the knapsack capacity as contraint

> *0/1 knapsack problem*
> A thief robbing a store wants to take the most valuable load that can be carried in a knapsack with a max capacity of $W$ kgs of loot. The thief can choose to take any set of n items in the store. Each item $i$ is worth $v_i$ dollars and weighs $w_i$ kgs. Which items should the thief take? 

***Logic:***
If the best solution at a max capacity $W$ has an item $j$ in it, then the rest of the items are actually the best solution for a max capacity $W$ - $w_j$
- This can be thought of in the other manner too. If we want to find the best solution for a capacity $W$, we should start from the minimum capacity and build our solution upwards. This is dynamic programming which runs in $\Theta(W*n)$
- A solution can be found using brute-force by computing every possible combination, which runs at $\Theta(n!)$ 

***Approach***
There are 2 ways to approach a dynamic programming problem, either bottom-up or top-down. Bottom-up uses a memory function to store solved values in a table while top-down uses memoization

*bottom-up*
```c
#include <stdio.h>

// Function to find the maximum of two integers
int max(int a, int b) {
    return (a > b) ? a : b;
}

// Function to solve 0/1 Knapsack Problem bottom-up approach
int knapsack(int W, int wt[], int val[], int n) {
    int i, w;
    int K[n+1][W+1];

    // Build table K[][] in bottom up manner
    for (i = 0; i <= n; i++) {
        for (w = 0; w <= W; w++) {
            if (i == 0 || w == 0)
                K[i][w] = 0;
            else if (wt[i-1] <= w)
                K[i][w] = max(val[i-1] + K[i-1][w-wt[i-1]],  K[i-1][w]);
            else
                K[i][w] = K[i-1][w];
        }
    }

    return K[n][W];
}

int main() {
    int val[] = {60, 100, 120};
    int wt[] = {10, 20, 30};
    int W = 50;
    int n = sizeof(val) / sizeof(val[0]);

    printf("Maximum value in knapsack = %d\n", knapsack(W, wt, val, n));
    return 0;
}
```

*top-down*
```c
#include <stdio.h>
#include <string.h>

// Function to find the maximum of two integers
int max(int a, int b) {
    return (a > b) ? a : b;
}

// Top-down (memoization) approach for 0/1 Knapsack
int knapsack(int W, int wt[], int val[], int n, int dp[][1001]) {
    if (n == 0 || W == 0)
        return 0;

    if (dp[n][W] != -1)
        return dp[n][W];

    if (wt[n-1] <= W)
        dp[n][W] = max(val[n-1] + knapsack(W-wt[n-1], wt, val, n-1, dp),
                       knapsack(W, wt, val, n-1, dp));
    else
        dp[n][W] = knapsack(W, wt, val, n-1, dp);

    return dp[n][W];
}

int main() {
    int val[] = {60, 100, 120};
    int wt[] = {10, 20, 30};
    int W = 50;
    int n = sizeof(val) / sizeof(val[0]);

    // dp[n+1][W+1], set all elements to -1
    int dp[4][1001];
    memset(dp, -1, sizeof(dp));

    printf("Maximum value in knapsack = %d\n", knapsack(W, wt, val, n, dp));
    return 0;
}
```


# Memory Functions
Used to calculate and store relevant values in memory
- Generally recursive
- Use top-down and bottom-up approach

```al
FUNC knapsack_memoryFn(i, j)
//INPUT: i is the object considered, j is the weight limit
//OUTPUT: optimal solution
	IF (V[i][j] == -1 ) //spot is unfilled/not calculated
		IF ( Weight[i] > j)  // item wt is greater than current limit
			V[i][j] = knapsack_memoryFn(i-1,j)
		ELSE
			V[i][j] = MAX( V[i-1][j] , V[i-1][j - Weight[i]] + Val[i] )
	END-IF
RETURN V[i][j]
```