Commonly used to solve optimization problems
- Problem should be solved in stages.
- Include all feasible solutions in final solution

```algorithm
ALGORITHM Greedy(a, n)
	FOR (i: 1 -> n)
		x = Select(a)
		IF x == Feasible
			Solution = Solution + x
		END IF
	END FOR
RETURN
```

## Knapsack Problem
Given n items of known weights w1, w2 , . . . , wn and values v1, v2 , . . . , vn and a knapsack of capacity W , find the most valuable subset of the items that fit into the knapsack.
- This is an NP-hard problem
1. **0/1 Knapsack Problem**: Each item can either be included or excluded from the knapsack. This version does not allow for fractional items.
2. **Fractional Knapsack Problem**: Items can be divided and a fraction of an item can be included in the knapsack.
**Greedy Algorithm** for the Knapsack Problem involves making the locally optimal choice at each step with the hope that these local choices will lead to a global optimum solution.
- **Greedy with Respect to Weight**:
    - Sort items by weight.
    - Select items starting from the lightest until the knapsack is full.
    - **Issue**: Does not always yield the optimal solution because lighter items might have lower total value.
- **Greedy with Respect to Profit**:
    - Sort items by profit
    - Select items starting from the most profitable until the knapsack is full.
    - **Issue**: Does not always yield the optimal solution because highly profitable items might be too heavy.
- **Greedy with Respect to Profit/Weight Ratio**
    - Sort items by profit/weight ratio.
    - Select items starting from the highest ratio until the knapsack is full.
    - **Fractional Knapsack**: This method guarantees an optimal solution for the fractional knapsack problem because it ensures that the most valuable items per unit of weight are chosen first.

## Huffman Coding
A compression technique used to reduce the size of data
