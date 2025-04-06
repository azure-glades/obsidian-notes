 ***Recursive function is a function that calls itself***
- Tail recursion: Recursive call is after applying logic
- Head recursion: Recursive call is before applying logic

Recursion is *top-down approach* to problem solving since it divides it into smaller sub problems and solves each of those sub problems by dividing them further, until it reaches the smallest base case where logic is applied 

Iteration is *bottom-up approach* where solving begins with what is known and is and builds up the main solution with that

Function calls are stored in **call stack**. Call stack stores the functions that are called in sequence. first in first out.
- When a function calls another function, the master function remains paused and waits until the slave function finishes.
- In recursion, the 1st recursive call is paused and waits until the recursive calls under it complete execution, which also have to wait until all recursive calls under them finish execution too

Recursion is usually slower than iterations because of repeated function calls needing to have memory allocated, while iterations use loops.

The advantage with recursion is how easy it is to develop and solve problems in recursion. The logic required is minimal.

There are multiple ways to analyse the efficiency of recursive functions {see also [[Efficiency Analysis]]}
##  Backward Substitution Method
Steps
1. **Expand the recurrence**: Substitute each term with its recursive definition.
2. **Identify the pattern**: Observe the emerging structure after multiple substitutions.
3. **Reach the base case**: Continue substitutions until the initial condition is reached.
4. **Sum terms**: Combine all terms to derive the final solution.
The final answer is the reduced form of the recurrence relation
> Example:$$T(n) = T(n-1) + n \quad \text{for } n > 1, \quad T(1) = 1$$
>5. **First substitution**:$T(n) = T(n-1) + n$
>    Substitute $T(n-1) = T(n-2) + (n-1)$: $T(n) = [T(n-2) + (n-1)] + n = T(n-2) + (n-1) + n$
> 6. **Second substitution**:
>    Substitute $T(n-2) = T(n-3) + (n-2)$:
>    $T(n) = T(n-3) + (n-2) + (n-1) + n$
> 7. **After $k$ substitutions**:$T(n) = T(n-k) + (n - k + 1) + \dots + (n-1) + n$
> 8. **Base case ($k = n-1$)**:
>    $T(n) = T(1) + 2 + 3 + \dots + n = 1 + \sum_{i=2}^n i = \frac{n(n+1)}{2}$
> Final answer:
> $T(n) \in O(n^2)$
> 
## Master’s Theorem
Master’s theorem is a theorem that narrows down the time complexity of algorithms of the form
$$T(n) = \alpha*T(\frac{n}{\beta})+f(n)$$
which are usually Divide and Conquer algorithms.
Here $f(n)$ is called the driving function, and $\alpha \ge 1$ and $\beta\gt1$  
> The time complexity of function $T(n)$ gets split into 3 possibilities based on how how $f(n)$ and the dividing function grow
>- We define the *watershed function* to characterize the time complexity of the dividing function i.e $$\text{watershed function(n)} =n^{\log_\beta(\alpha)}$$
1. **Case 1:**  If there exists a constant $\epsilon > 0$ such that $f(n) \in O(n^{\log_\beta \alpha-\epsilon})$, then:
   $$
   T(n) \in \Theta(n^{\log_\beta \alpha})
   $$

2. **Case 2:** If there exists a constant $k \geq 0$ such that $f(n) = \Theta(n^{\log_\beta \alpha} *(\log n)^k)$, then:
   $$
   T(n) = \Theta(n^{\log_\beta \alpha} *(\log n)^{k+1})
   $$

3. **Case 3: with Regularity Condition** If there exists a constant $\epsilon > 0$ such that $f(n) = \Omega(n^{\log_\beta \alpha + \epsilon})$, and if $f(n)$ additionally satisfies the *regularity condition* $af(n/b) \leq cf(n)$ for some constant $c < 1$ and all sufficiently large $n$, then:
   $$
   T(n) = \Theta(f(n))
   $$
## Recursion Tree
The recursion tree method is a visual approach to solve recurrence relations by representing the recursive calls as a tree. Each node in the tree corresponds to the cost incurred at a specific level of recursion, and the total cost is calculated by summing up the costs across all levels.
Consult: [GRS](https://youtu.be/jvA6fOafhGs?feature=shared)
