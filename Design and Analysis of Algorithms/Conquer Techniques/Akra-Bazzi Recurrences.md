A type of recurrences that takes the form:
$$\displaylines{
T(n) = f(n) + \sum_{i = 1}^{k}a_iT(n/b_i) \\ \text{where } k \in \mathbb{Z}^+; a_i,b_i \in \mathbb{R}, a_i > 0 \text{ and } b_i > 1}
$$
is called an Akra-Bazzi recurrence.
- The driving function $f(n)$ satisfies the *polynomial growth condition*
> Polynomial growth condition: $f(\Theta(n)) = \Theta(f(n))$

The solution to Akra-Bazzi recurrence is given by:
$$
T(n) = \Theta\left( n^p \left(1 + \int_1^n \frac{f(x)}{x^{p+1}} \, dx \right) \right)
$$
Where $n^p$: Dominant polynomial term, where $p$ solves $\sum_{i=1}^k a_i b_i^p = 1$
(pg 117 for examples)
