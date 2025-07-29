A *Decision Problem* is the kinds of problems that can be posed as [yes–no questions](https://en.wikipedia.org/wiki/Yes%E2%80%93no_question "Yes–no question")
![[Pasted image 20250629233620.png|200]]



> **Definition 1:** Polynomial Time
> An algorithm $F(n)$ is said to be solvable in polynomial time when  $$ \text{worst-case of }F(n) \in O(p(n))$$  where $p(n)$ is a polynomial

> **Definition 2:** Class P
> Class $P$ is a class of decision problems that can be solved in polynomial time.
> $$F(n) \in P \implies \text{worst-case of }F(n) \in O(p(n))$$

> **Definition 3:** Non-deterministic algorithms
> An algorithm that solves a decision problem by :
> (i) Guessing a solution non-deterministically
> (ii) Checks/Determines whether the solution is correct in polynomial time
> 
> Technically the definition involves Turing machines. So, a non-deterministic algorithm is
> (i) Solvable in poly-time by a [Non-deterministic Turing Machine](https://en.wikipedia.org/wiki/Nondeterministic_Turing_machine)
> (ii) Verifiable in poly-time by a [Deterministic Turing Machine](https://en.wikipedia.org/wiki/Turing_machine)

> **Definition 4:** Class NP
> Class $NP$ is a class of decision problems that can be solved by non-deterministic polynomial-time algorithms

**Theorem:** 
$$ P \subseteq NP$$
Unsolved problem in computer science, *If the solution to a problem is easy to check for correctness, must the problem be easy to solve?*. Current belief is that $P \ne NP$
![[Pasted image 20250629232101.png]]

> **Definition 5:** Polynomial Reducibility
> A decision problem $D$ is said to be polynomially reducible if there exists a transformation $T: D \to F$ where 
> (i) $T$ is an isomorphism 
> (ii) The transformation function is computable in polynomial time
> (iii) $F \in P$ 
> We need-not know the polynomial-time solution of $D$ but if it is polynomially reducible, it means there does exist a poly-time solution

> **Definition 6:** NP-complete
> A decision problem $D$ is said to be NP-complete if
> (i) $D \in NP$
> (ii) $D$ is polynomially reducible