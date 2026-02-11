Local Beam Search is a **heuristic local search algorithm** that attempts to overcome the primary limitation of Hill-Climbing (getting stuck in local optima) by exploring **multiple states simultaneously**.

It works by maintaining a fixed-size set of the best candidate solutions at each step, referred to as the **beam**

## How Local Beam Search Works
Local Beam Search (LBS) can be thought of as running k parallel hill-climbing searches that communicate with each other.
### 1. Initialization
The algorithm starts with *k (the beam width)* randomly generated initial states.
### 2. Successor Generation
All successor states (neighbors) are generated for _all_ k current states. If the beam width is k and the *average branching factor is b*, this creates a pool of up to `k x b` successor states.
### 3. Selection (The Key Step)
Instead of returning to its original "parent" state, the algorithm evaluates _all_ `k x b` successor states using the objective/heuristic function and **selects the k best states** from this entire pool to form the next set of current states.
- This selection is what allows the k parallel searches to **share information**. If one search thread finds a promising area, the k best states selected might all be successors of that single good thread, effectively **abandoning** the less promising threads and concentrating the entire search effort in the best region.
### 4. Termination
The process repeats until a goal state is found or a termination condition (like a maximum number of iterations) is met.

## LBS vs. Other Searches

| **Comparison**          | **k=1 (Beam Width of 1)**                       | **Independent Hill-Climbing**                                                          | **LBS (k>1)**                                                                 |
| ----------------------- | ----------------------------------------------- | -------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| **Algorithm**           | **Hill-Climbing Search**                        | $k$ separate Hill-Climbing searches                                                    | **Local Beam Search**                                                         |
| **Search States**       | 1 state                                         | $k$ states, searched independently                                                     | $k$ states, searched cooperatively                                            |
| **Information Sharing** | None                                            | None                                                                                   | **Yes**: The best successors from _all_ $k$ states are pooled.                |
| **Vulnerability**       | High risk of getting stuck in **local optima**. | High risk of all $k$ searches getting stuck in the _same_ or _different_ local optima. | **Reduced risk**: A good thread can pull the entire search out of a bad area. |

# Stochastic Local Beam Search
A common variation, **Stochastic Local Beam Search**, addresses the issue where the $k$ selected states might quickly become very similar, essentially collapsing the search into a single Hill-Climbing run.
- Instead of deterministically selecting the absolute _best_ $k$ states, it selects $k$ states **at random**, but the **probability** of selecting a state is weighted by its heuristic value. This maintains a degree of diversity, helping the algorithm explore a broader area and reduce the chance of premature convergence.

Local Beam Search is a valuable technique for optimization that balances the simplicity of hill-climbing with a parallel approach to escape local maxima.