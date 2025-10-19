A classical problem that can be solved using backtracking or dynamic programming.

Given a set of numbers $A$ and a target sum $t$, check if there exists $B \subseteq A$ whose elements add up to $t$

## [[Dynamic Programming]] Approach

## Backtracking Approach
## Backtracking Approach
Backtracking systematically explores all possible subsets by building them incrementally. If at any point the current subset cannot possibly lead to a solution (e.g., the sum exceeds ), the algorithm abandons that path (backtracks) and tries another possibility.

### Algorithm Steps
1. **Start with an empty subset and sum 0 at index 0.**
2. **For each element at the current index:**
   - **Include** the element in the current subset and add its value to the current sum.
   - **Recurse** to the next index.
   - **Exclude** the element from the subset (backtrack) and recurse to the next index.
3. **If the current sum equals the target sum \( S \), record the current subset as a solution.**
4. **If the current sum exceeds \( S \) or all elements are considered, backtrack.**

> State space tree
> - Each node represents a decision: include or exclude the current element.
> - The tree explores all possible combinations (subsets).

```al
FUNC sumOfSubsets(runningSum, cur, backSum)
//INPUT: S is the main set, cur is current element, backSum is for backtracking, runningSum is compared
// OUTPUT: return subset that meets target
	x[k] = 1;
	IF( S[k] + runningSum == target)
		print(x)
	ELSE IF( S[k] + S[k+1] + runningSum <= target)
		sumOfSubsets(S[k] + runningSum, k+1, backSum - S[k])
	//
	IF(runningSum + backSum-S[k] > target)AND(runningSum + S[k+1] <= target)
		x[k] = 0     //exclude element
		sumOfSubsets(runningSum, k+1, backSum - W[k])
RETURN
```

### Time Complexity
- **Worst-case:** $O(2^n)$
- **Pruning:** If the sum exceeds, that branch is abandoned early, which can improve practical performance.

``` c
#include <stdio.h>

#define N 4 // Number of elements in the set

void printSubset(int subset[], int size) {
    printf("{ ");
    for (int i = 0; i < size; i++)
        printf("%d ", subset[i]);
    printf("}\n");
}

void sumOfSubsets(int arr[], int subset[], int n, int subsetSize, int total, int index, int target) {
    if (total == target) {
        printSubset(subset, subsetSize);
        // Continue searching for other solutions
        return;
    }
    if (index == n || total > target)
        return;

    // Include current element
    subset[subsetSize] = arr[index];
    sumOfSubsets(arr, subset, n, subsetSize + 1, total + arr[index], index + 1, target);

    // Exclude current element (backtrack)
    sumOfSubsets(arr, subset, n, subsetSize, total, index + 1, target);
}

int main() {
    int arr[N] = {3, 4, 5, 2};
    int subset[N];
    int target = 9;

    printf("Subsets of sum %d are:\n", target);
    sumOfSubsets(arr, subset, N, 0, 0, 0, target);
    return 0;
}
```
## Key Points
- Backtracking is a brute-force search with pruning: it abandons paths that cannot yield a solution.
- The approach is recursive and explores all possible subsets.
- Pruning (stopping when the sum exceeds the target) makes the algorithm more efficient than pure brute force.

## Applications
- Partition problems
- Knapsack problems
- Any scenario requiring enumeration of all valid combinations under constraints
