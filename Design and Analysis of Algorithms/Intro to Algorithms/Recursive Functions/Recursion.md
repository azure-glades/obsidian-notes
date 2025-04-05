***Recursive function is a function that calls itself***
- Tail recursion: Recursive call is after applying logic
- Head recursion: Recursive call is before applying logic

Recursion is *top-down approach* to problem solving since it divides it into smaller sub problems and solves each of those sub problems by dividing them further, until it reaches the smallest base case where logic is applied 

Iteration is *bottom-up approach* where solving begins with what is known and is and builds up the main solution with that

Function calls are stored in **call stack**. Call stack stores the functions that are called in sequence. first in first out.
- When a function calls another function, the master function remains paused and waits until the slave function finishes.
- In recursion, the 1st recursive call is paused and waits until the recursive calls under it complete execution, which also have to wait until all recursive calls under them finish execution too

Recursion is usually slower than iterations because of repeated function calls needing to have memory allocated, while iterations use loops.

There are multiple ways to analyse the efficiency of recursive functions {see also [[Efficiency Analysis]]}
##  Substitution Method

## Master’s Theorem
Master’s theorem is a theorem that narrows down the time complexity of algorithms of the form
$$T(n) = \alpha*T(\frac{n}{\beta})+f(n)$$
which are usually [[Divide and Conquer]] algorithms.
Here $f(n)$ is called the driving function, and $\alpha \ge 1$ and $\beta\gt1$  
> The function $T(n)$ gets split into 
## Recursion Tree
l
