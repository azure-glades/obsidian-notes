Dynamic programming solves problems by combining the solutions to subproblems. Programming refers to tabulation of the solutions.
Divide-and-conquer solves problems by dividing into distinct non-overlapping subproblems. Dynamic programming works even when subproblems overlap by storing the solutions in a table. It then consults the table to arrive at the optimal solution.

> Dynamic Programming = Recursion + Memoization. 

[DP - MIT](https://youtu.be/r4-cftqTcdI?feature=shared) Legit video, SRTBOT

Dynamic programming is commonly applied to *optimization problems*
Steps:
1. Characterize the structure of optimal solution
2. recursively define optimal solution
3. compute optimal solution (bottom up)
4. construct optimal solution from computed info

> DP is technically a DFS through a reverse subproblem Graph (think about it)

Ex:
> *Algorithms:*
> [[Bellman-Ford Algorithm]]
> [[Floyd-Warshall Algorithm]]
> [[Johnson’s Algorithm]] - For sparse matrices
> [[Kadane’s Algorithm]]
> *Problems:*
> [[Dynamic Programming/Knapsack problem]] and [[Fractional Knapsack Problem]]
> [[Rod Cutting Problem]]
> *Techniques:*
> [[Binomial Coefficient]]


Fibonacci problem can be done using dynamic programming → memoization and tabulation method
## **What Are Memory Functions?**
- A memory function is a function that remembers (stores) the result of each subproblem it solves.
- When the function is called with the same arguments again, it returns the stored result instead of recomputing it.
- This avoids redundant calculations and improves efficiency, especially for problems with overlapping subproblems.

>Some syllabi introduce DP in a _bottom-up_ (tabulation) way first, treating _top-down_ (memoization) as an alternative approach later.
>- **Memoization is Inherent to DP** – Top-down DP _is_ recursion + memoization. Without memory functions, you’re just doing brute-force recursion.
>- **DP is More Than Just Memoization** – Some DP problems are better solved with _tabulation_ (iterative DP), so memoization isn’t always the focus.
#### **Memoization (Top-Down DP)**
- **What it is**: Optimizing a recursive solution by caching results of subproblems to avoid redundant computations.  
- **How it works**:  
  - Start from the original problem and break it down recursively.  
  - Store results of subproblems in a lookup table (e.g., array, hashmap).  
  - Before computing a subproblem, check if it’s already solved.  
- **Example**: Fibonacci sequence with memoization.  
  ```python
  memo = {}
  def fib(n):
      if n in memo: return memo[n] # check if it is stored
      if n <= 1: return n          # base case
      memo[n] = fib(n-1) + fib(n-2) # recursive case and store
      return memo[n]
  ```

#### **Tabulation (Bottom-Up DP)**
- **What it is**: Solving the problem iteratively by filling a table (usually an array) from the smallest subproblems up.  
- **How it works**:  
  - Define the order in which subproblems are solved (often from base cases up).  
  - Fill the table iteratively, referencing prior entries.  
- **Example**: Fibonacci sequence with tabulation.  
  ```python
  def fib(n):
      dp = [0, 1] + [0] * (n-1)
      for i in range(2, n+1):
          dp[i] = dp[i-1] + dp[i-2]
      return dp[n]
  ```

| **Memoization (Top-Down)** | **Tabulation (Bottom-Up)** |
|----------------------------|----------------------------|
| More intuitive (follows natural recursive structure). | Requires explicit definition of evaluation order. |
| Only computes necessary subproblems (*lazy evaluation*). | Computes *all* subproblems, even unused ones. |
| Can suffer from recursion stack overhead (stack overflow for large inputs). | No recursion, so better for deep call stacks. |
| Harder to optimize for space (unless using techniques like memoization with pruning). | Easier to optimize space (e.g., reusing a 1D array). |
| Works well when subproblems are not easily ordered (e.g., tree/graph DP). | Works best when subproblems have a clear order (e.g., strings, arrays). |

- **Memoization** is the *bridge* between brute-force recursion and DP. It’s the first optimization step.  
- **Tabulation** is often more efficient (constant factors matter in competitive programming) but requires deeper insight into the problem structure.  
- Some problems are *far easier* to solve with one approach over the other:  
  - **Memoization shines**: Problems where subproblems are sparse (e.g., "given a tree, find the longest path").  
  - **Tabulation shines**: Problems with clear dependencies (e.g., "edit distance between two strings").  
