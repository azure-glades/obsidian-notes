Both Hill-Climbing Search and Simulated Annealing are types of **Local Search Algorithms** used for **optimization problems**. They search for the best solution state (highest value or lowest cost) by iteratively moving from a current state to a neighboring state, guided by a heuristic (objective function).

## Hill-Climbing Search
Hill-Climbing Search is the simplest local search algorithm, inspired by a climber who tries to reach the peak of a mountain by always taking a step in the direction of the steepest ascent.
### Key Characteristics:
1. **Greedy Approach:** At every step, the algorithm is purely **greedy**.4 It evaluates all neighboring states and chooses the one that offers the **best immediate improvement** in the objective function.
2. **No Backtracking:** It keeps track of only the current state and never looks back or considers the path taken.
3. **Termination:** It stops when it reaches a state where **no neighboring state has a better value**. This point is called a **peak**.
### Major Problem: Local Optima
The main drawback of Hill-Climbing is that it can get stuck in a **local maximum** (or minimum) and fail to find the **global maximum** (the true best solution).
- **Local Maximum:** A state that is better than all of its neighbors, but is worse than the global maximum in the entire search space.
- **Plateau:** A flat area where all neighboring states have the same value, providing no direction to move.
- **Ridge:** A sequence of local maxima that create a narrow, difficult path to the global optimum.

### Variations
- stochastic hill climb - randomly choose among good moves, dont always take the steepest/best
- first choice hill climb - generate successors randomly and take the first good successor u make (even if its not the best)
- Random restart hill climb - do hill climb multiple times from different start locations
![[Pasted image 20260111120809.png]]

## Simulated Annealing
Simulated Annealing (SA) is a variation of Hill-Climbing that overcomes the problem of local optima by introducing a controlled amount of **randomness**. It is inspired by the **annealing process** in metallurgy, where a material is heated and then slowly cooled to allow its atoms to settle into a minimal-energy, highly ordered crystalline structure.
### Key Mechanism: Temperature -> Randomness decreases over time
The crucial difference is that SA doesn't always move to a better neighbor; it allows the algorithm to occasionally take a **"bad" move** (a move to a state with a lower objective value).
- **Temperature (T):** A variable that controls the probability of accepting a bad move.$T$ starts high and slowly decreases (the **cooling schedule**).
    - **High $T$ (Start):** The probability of accepting a worse move is **high**, allowing the algorithm to broadly **explore** the search space and jump out of local optima.
    - **Low $T$ (End):** The probability of accepting a worse move is **low**, making the algorithm behave like Hill-Climbing, settling into a deep minimum (or maximum) to **exploit** the best region found.

The probability of accepting a worse move, $\Delta E$, is often calculated using the Metropolis Criterion:$$P(\text{accept}) = e^{-\Delta E / T}$$
where $\Delta E$ is the positive difference in the objective value (the "badness" of the move).
![[Pasted image 20260111120750.png]]
### SA vs. Hill-Climbing: The Main Difference

| **Feature**          | **Hill-Climbing Search**                            | **Simulated Annealing (SA)**                                                                               |
| -------------------- | --------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Move Rule**        | **Only accepts improving moves** (strictly greedy). | Accepts **improving moves always**; accepts **worsening moves probabilistically**.                         |
| **Randomness**       | None (unless a stochastic variant is used).         | **Controlled randomness** via the **Temperature** $T$.                                                     |
| **Risk**             | **Gets stuck** easily in local optima.              | Can **escape local optima** to find the global optimum (given a slow enough cooling schedule).             |
| **Global Optimum19** | Not guaranteed to find it.                          | **Guaranteed** to find the global optimum if $T$ decreases slowly enough (a strong theoretical guarantee). |
