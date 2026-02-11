The **Genetic Algorithm (GA)** is a powerful **local search and optimization technique** inspired by the process of **natural selection and genetics** (biological evolution). It is used to find high-quality solutions to optimization and search problems by evolving a population of candidate solutions.

It falls under the category of **evolutionary algorithms** and is particularly effective for problems where the search space is large and complex, or where a traditional mathematical approach is too difficult.

| **Term**                  | **Biological Analogy**           | **GA Interpretation**                                                                                                                       |
| ------------------------- | -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **Individual/Chromosome** | A living organism                | A single **candidate solution** to the problem, typically represented as a binary string (a sequence of 0s and 1s) or a list of parameters. |
| **Population**            | A group of organisms             | The set of candidate solutions used in one iteration of the search.                                                                         |
| **Gene**                  | A trait-determining unit         | A single unit (bit or variable) within the chromosome.                                                                                      |
| **Fitness Function**      | Ability to survive and reproduce | The **objective function** or **heuristic** that measures the quality of a solution. Higher fitness means a better solution.                |
## The Genetic Algorithm Cycle
A GA starts with a random population and proceeds through iterative steps, called **generations**, until a satisfactory solution is found or a maximum number of generations is reached.
#### 1. Initialization
A starting population of $N$ chromosomes (candidate solutions) is created, usually by generating them **randomly**.
#### 2. Evaluation
Every individual in the current population is evaluated using the **Fitness Function**. The fitness value determines how good the solution is.
#### 3. Selection (Survival of the Fittest)
A portion of the current population is selected to be **parents** for the next generation.
- Selection is typically based on fitness: individuals with **higher fitness** have a greater probability of being chosen. 
Common methods include Roulette Wheel Selection or Tournament Selection.
#### 4. Genetic Operators (Creating Offspring)
The chosen parents are then used to create new offspring (the next generation) through two main genetic operations:

***A. Crossover (Recombination)***
This operation mimics biological reproduction.13 Two parent chromosomes exchange genetic information to create two new offspring chromosomes.14
- **Example (Single-point Crossover):**
    - Parent 1: $\mathbf{1 1 0} \mid \mathbf{1 010}$
    - Parent 2: $\mathbf{0 0 1} \mid \mathbf{0111}$
    - Offspring 1: $\mathbf{1 10} \mid \mathbf{0111}$ (Inherits first part of P1, second part of P2)
    - Offspring 2: $\mathbf{001} \mid \mathbf{1010}$ (Inherits first part of P2, second part of P1)

***B. Mutation***
This operation introduces random, small changes to a chromosome. This ensures **diversity** in the population and prevents the algorithm from getting stuck in a local optimum (similar to the role of the random walk in Simulated Annealing).
- **Example (Bit-Flip Mutation):**
    - Original: $10110010$
    - Mutated (Flip 4th bit): $101\mathbf{0}0010$
#### 5. Replacement and Termination
The new offspring population replaces the old one. The cycle repeats from **Step 2** until a termination condition is met (e.g., the best solution reaches a certain fitness threshold, or a maximum number of generations has been completed).

GA is highly effective for complex problems like scheduling, machine learning hyperparameter tuning, and optimal design, as it explores the search space globally while constantly improving the current best solutions.

![[Pasted image 20260111121910.png]]