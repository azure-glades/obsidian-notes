# Premise
Binomial Coefficient = $${n \choose {r}} = {n-1 \choose {r-1}} + {n-1 \choose {r}}$$
Since it can be precalculated, this is a problem solved by dynamic programming
Base cases: $C(n,0) = 1$ and $C(n,n) = 1$

Easily solved by computing a table `memo[][]` where $$\text{memo}[i][j] = C(i,j)$$
# Algorithm Steps
1. Initialize a 2D array `dp[n+1][k+1]`
2. Set `dp[i]][0] = 1` and `dp[i][i] = 1`
3. Fill up the table with the formula `dp[i][j] = dp[i-1][j] + dp[i-1][j-1]`
4. Alternatively : Call `dp[n][k]` and start filling recursively

Algo
```c
#include <stdio.h>

int binomialCoefficient(int n, int k) {
    int dp[n+1][k+1];
    
    for (int i = 0; i <= n; i++) {
        for (int j = 0; j <= (i < k ? i : k); j++) {
            if (j == 0 || j == i)
                dp[i][j] = 1;
            else
                dp[i][j] = dp[i-1][j-1] + dp[i-1][j];
        }
    }
    return dp[n][k];
}

int main() {
    int n = 5, k = 2;
    printf("C(%d, %d) = %d\n", n, k, binomialCoefficient(n, k));
    return 0;
}

```

# Complexity Analysis
Time: $O(n*k)$ 
Space: $O(n*k)$