***What is efficiency of algorithms***

1. Space efficiency
2. Time efficiency

> *Definitions*
> - **Basic Operations**: The most important (and repeated) operation in the algorithm is a basic operation
> - **Worst case, Best case and Average case**: The case for which the algorithm runs the longest, quickest, and for a typical (random) case.
> - The **order of growth** in algorithms refers to the asymptotic behavior of an algorithm's resource requirements (such as time or space) as the size of the input grows.
> *See further: [Amortized Efficiency](https://en.wikipedia.org/wiki/Amortized_analysis)*

## Efficiency classes
- **Constant ($O(1)$)**: The runtime does not change with input size.  
  Example: Accessing an array element.
- **Logarithmic ($O(\log n)$)**: The runtime grows slowly as the input size increases.  
  Example: Binary search.
- **Linear ($O(n)$)**: The runtime grows proportionally to the input size.  
  Example: Iterating through a list.
- **Linear Logarithmic ($O(n \log n)$)**: Often seen in efficient algorithms like sorting.  
  Example: [[Merge sort]], [[Quick sort]]
- **Quadratic ($O(n^2)$)**: The runtime grows with the square of the input size.  
	- Example: Nested loops like [[Selection sort]], [[Insertion sort]], [[Bubble sort]]
	- [[Distinct Elements in Array]], [[Decimal to Binary]]
- **Qubic** $O(n^3)$: Qubic runtimes when 3 loops are used, like [[Matrix Multiplication]].
- **Exponential ($O(2^n)$)**: The runtime doubles with each unit increase in input size.  
  Example: Brute-force algorithms.
-> Think about how the algo performs with growing input size -> Orders of growth
Order is used to rank the algorithm
- *Asymptotic notation* is used for comparing and ranking algorithms

## Asymptotic Notation
 ***A notation used in comparing and ranking the performance of algorithms***
1. Big O <=          → Upper bound
2. Big $\Omega$  >=         → Lower bound
3. $\Theta$ =                   → Average bound
4. Small o <
5. Small $\omega$ >
These are *not* related to worst case, avg case, best case of algos
### Big O notation
- O(g(n)) is the upper bound , i.e f(n) will not take more time than g(n)
A function $t(n)$ is said to be in $O(g(n))$, denoted as $t(n) \in O(g(n))$, if $t(n)$ is bounded above by some constant multiple of $g(n)$ for all large $n$. Formally, this means there exist some positive constant $c$ and some nonnegative integer $n_0$ such that:
$$
t(n) \leq c \cdot g(n)
$$
for all $n \geq n_0$.

If $f(n) = O(n)$, then it is also true that:
- $f(n) = O(n^2)$
- $f(n) = O(n!)$

This is because Big-O notation describes an **upper bound** on the growth of a function. If $f(n)$ grows no faster than $n$, it will also grow no faster than $n^2$ or $n!$.

However, **we generally prefer the tightest (lowest) upper bound** to describe the growth of a function. Therefore, we would typically write $f(n) = O(n)$ instead of $f(n) = O(n^2)$ or $f(n) = O(n!)$, as $O(n)$ provides the most precise and useful information about the function's growth rate.
### Big $\Omega$ notation
- $\Omega(g(n))$ is the lower bound, i,e f(n) will take more time than g(n) 
A function $t(n)$ is said to be in $\Omega(g(n))$, denoted as $t(n) \in \Omega(g(n))$, if $t(n)$ is bounded below by some positive constant multiple of $g(n)$ for all large $n$. Formally, this means there exist some positive constant $c$ and some nonnegative integer $n_0$ such that:

$$
t(n) \geq c \cdot g(n)
$$

for all $n \geq n_0$.
if $f(n) \in \Omega(n)$  then $f(n) \in \Omega(\log n), f(n) \in \Omega(1)$ is correct

### $\Theta$ notation
- $\Theta(g(n))$ is average notation, i.e f(n) will take around the same time as g(n) to complete
A function $t(n)$ is said to be in $\Theta(g(n))$, denoted as $t(n) \in \Theta(g(n))$, if $t(n)$ is bounded **both above and below** by some positive constant multiples of $g(n)$ for all large $n$. Formally, this means there exist some positive constants $c_1$ and $c_2$ and some nonnegative integer $n_0$ such that:

$$
c_2 \cdot g(n) \leq t(n) \leq c_1 \cdot g(n)
$$

for all $n \geq n_0$.
if $f(n) \in \Theta(g(n))$ then $f(n) \in O(g(n))$ and $f(n) \in \Omega(g(n))$ is also true 


> [!important] Limits
> Limits to compare orders of growth $$\lim_{n\rightarrow\infty} \frac{f(n)}{g(n)}=c$$
> if c = 0, then f(n) has a smaller order of growth than g(n) » $f(n)\in O[g(n)]$     
> if c = constant, then f(n) has same order of growth as g(n) » $f(n)\in \Theta[g(n)]$
> if c = infinity, then f(n) has a higher order of growth than g(n) » $f(n)\in \Omega[g(n)]$

## Properties
- **Scaling:** If $f(n)$ is $O(g(n))$, then $f(n)$ is also $c \cdot O(g(n))$ for any constant $c$. This holds for all three notations: $O$, $\Omega$, and $\Theta$.
- **Reflexive:** For any function $f(n)$, $f(n)$ is $O(f(n))$. This means any function is an upper bound of itself. This property holds for all three notations.
- **Transitive:** If $f(n)$ is $O(g(n))$ and $g(n)$ is $O(h(n))$, then $f(n)$ is also $O(h(n))$. This property holds for all three notations.
- **Symmetric:** If $f(n)$ is $\Theta(g(n))$, then $g(n)$ is $\Theta(f(n))$. This property is **only true for $\Theta$**.
- **Transpose Symmetric:** If $f(n)$ is $O(g(n))$, then $g(n)$ is $\Omega(f(n))$.
- **Theta Equivalence:** If $f(n)$ is $O(g(n))$ and $f(n)$ is also $\Omega(g(n))$, then $f(n)$ is $\Theta(g(n))$. This also holds in reverse.
- **Sum of Functions:** If $f(n)$ is $O(g(n))$ and $p(n)$ is $O(q(n))$, then $f(n) + p(n)$ is $O(\max[g(n), q(n)])$.
- **Product of Functions:** If $f(n)$ is $O(g(n))$ and $p(n)$ is $O(q(n))$, then $f(n) \cdot p(n)$ is $O(g(n) \cdot q(n))$.

---
## Properties
- if f(n) is O(g(n)) then f(n) is also c\*O(g(n)) → holds for all 3 notations
- *Reflexive:* if f(n) is given then f(n) is O(f(n)), i.e any function is the upper bound of itself → holds for all 3 notations
- *Transitive* : f(n) is O(g(n)) and g(n) is O(h(n)) then f(n) is also O(h(n))  → holds for all 3 notations
- *Symmetric:* f(n) is Theta(g(n)) then g(n) is Theta(f(n)) →Only true for Theta
- *Transpose symmetric::* if f(n) is O(g(n)) then g(n) is Omega(f(n)).
- if f(n) is O(g(n)) and f(n) is also Omega(g(n)) then f(n) is also Theta(g(n)). This also holds true in reverse
- if f(n) is O(g(n)) and p(n) is O(q(n)) then `f(n) + p(n)` is `O(max(g(n), q(n)))`
- if f(n) is O(g(n)) and p(n) is O(q(n)) then `f(n) * p(n)` is `O(g(n)*q(n))`
