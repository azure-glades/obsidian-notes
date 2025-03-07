
> *Definitions*
> - Basic Operations: The most important (and repeated) operation in the algorithm is a basic operation
## Asymptotic Notation
*Efficiency Classes*
1. constant 1
2. linear n
3. quadratic n^2
4. logarithm log(n)
5. qubic n^3
6. exponential x^n
7. factorial n!
n is the number of operations that are repeated the most. 
-> Think about how the algo performs with growing input size -> Orders of growth
Order is used to rank the algorithm
- *Asymptotic notation* is used for comparing and ranking algorithms
	1. Big O <=
	2. Big $\Omega$  >=
	3. $\Theta$ =
	4. Small o <
	5. Small $\omega$ >
Orders of growth, f(n) -> our algo, g(n) -> efficiency.
f(n) <= c.g(n), c > 0

> Asked perplexity to explain
![[Pasted image 20250305120550.png]]

- Big O represents an upper bound
- If i say time complexity of an algo is O(n^2) it means that the time taken will not exceed O(n^2)

- Big Omega represents a lower bound $f(n) \ge c*g(n), \forall c \gt 0$


## Aspects of Analysis
### 1. Understand the Problem
Before designing an algorithm, it's crucial to thoroughly understand the problem at hand. This involves:
- Clearly defining the input and desired output
- Identifying any constraints or special cases
- Breaking down complex problems into smaller, manageable subproblems
### 2. Ascertain Computational Device Capabilities
Consider the capabilities of the computational device that will execute the algorithm:
- Available memory and processing power
- Supported operations and data structures
- Any hardware-specific optimizations or limitations
	- For example, recursive algorithms may fail on devices with limited stack space
### 3. Exact vs. Approximate Solutions
Decide whether an exact solution is required or if an approximation is acceptable:
- Exact solutions may be computationally expensive for certain problems
- Approximation algorithms can provide faster results with acceptable accuracy
- Consider the trade-offs between precision and efficiency

- **Exact**: Guarantees optimal solutions (e.g., Dijkstra’s algorithm for shortest paths).
- **Approximate**: Faster but suboptimal (e.g., greedy algorithms for NP-hard problems like the Traveling Salesman Problem)
### 4. Algorithm Design Techniques
There are categorizes core strategies:
- **Brute Force** (e.g., checking all permutations).
- **Divide-and-Conquer** (e.g., Merge Sort).
- **Transform-and-Conquer** (e.g., presorting data).
- **Space-Time Tradeoffs** (e.g., hash tables for faster lookups)
- **Dynamic programming:** Solve subproblems once and store their solutions
- **Backtracking:** Explore all potential solutions by trying different choices
### 5. Design Data Structures
Choose appropriate data structures that complement the algorithm:
- Arrays, linked lists, trees, graphs, hash tables, etc.
- Consider time and space complexity trade-offs
- Optimize for the most frequent operations in the problem
### 6. Specify the Algorithm
Clearly communicate the algorithm using:
- Pseudocode: A high-level description of the algorithm's steps
- Flowcharts: Visual representation of the algorithm's logic
- Programming language: Formal implementation in a specific language
### 7. Prove Correctness
Ensure the algorithm produces correct results:
- Use mathematical induction or loop invariants
- Test with various input cases, including edge cases
- Formal verification techniques for critical application
### 8. Analyze Efficiency
- **Time complexity**: Measure steps using Big-O notation (e.g., _O(n²)_ for bubble sort).
- **Space complexity**: Memory usage (e.g., _O(1)_ for in-place sorting).
- Levitin highlights worst-case, best-case, and average-case analysis
### 9. Code the Algorithm
- Translate design into code while preserving efficiency.
- Avoid pitfalls like redundant computations (e.g., precompute values in dynamic programming)
- Choose an appropriate language for the task
---
