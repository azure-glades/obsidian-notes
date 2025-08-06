This lecture, "Artificial Intelligence for Economics - Lecture 9," by Assistant Professor Addoi Mitro, builds on the previous discussion of heuristic search by introducing the concepts of **game trees**, **multi-objective search**, and advanced optimization techniques. The goal is to apply these AI methods to model and solve complex economic problems.

---

### Gist of the Video

The lecture starts by framing sequential games like chess as a problem of finding an optimal path through a **game tree**. It introduces the **Minimax algorithm** to find the best possible outcome for a player, assuming the opponent also plays optimally. A key optimization to this is **Alpha-Beta Pruning**, which drastically reduces computation by ignoring irrelevant parts of the tree. The video then extends these ideas to scenarios with more than one objective, introducing **multi-objective heuristic search** and **multi-objective game trees**. In these cases, the cost is a vector, and decisions are made based on concepts like **Pareto dominance**, where one option is better than another across all criteria. Finally, the lecture connects these advanced search techniques to real-world economic applications, such as market competition, behavioral economics, and macroeconomic policy-making.

---

### Vital Topics and Key Points Discussed

#### 1. Game Trees: Modeling Strategic Interactions

- **Sequential Games:** Games like chess or tic-tac-toe are used as examples where two players take turns, and their objectives are opposite.
    
- **Game Tree Structure:** The game is represented as a tree where each **node** is a state (e.g., a board configuration), and **edges** are possible moves.
    
- **Player Objectives:**
    
    - **Player 1 (P1):** Aims to **minimize** the heuristic value (low value is good).
        
    - **Player 2 (P2):** Aims to **maximize** the heuristic value (high value is good).
        
- **Heuristic Values:** Each node in the tree has a heuristic value indicating its desirability for a particular player. The leaf nodes have final utility values.
    

#### 2. The Minimax Algorithm

- **Optimal Strategy:** Minimax is an algorithm used to find the optimal move for a player, assuming the opponent also plays optimally.
    
- **Bottom-up Propagation:** The algorithm works by propagating values from the leaf nodes up to the root.
    
- **Minimax Principle:**
    
    - At a **MAX** layer (P2's turn), the parent node takes the **maximum** value of its children.
        
    - At a **MIN** layer (P1's turn), the parent node takes the **minimum** value of its children.
        
- **Result:** The value at the root of the tree represents the best possible outcome for the starting player, assuming perfect play from both sides.
    

#### 3. Alpha-Beta Pruning: Optimizing the Search

- **Efficiency:** Minimax can be computationally expensive as it evaluates the entire game tree.
    
- **Pruning:** Alpha-Beta Pruning is an optimization that avoids exploring parts of the tree that are irrelevant to the final decision.
    
- **Alpha-Pruning:** In a **MIN** layer, if the algorithm finds a branch that is already worse than a previously found option (a value of **alpha**), it can prune the remaining branches of that subtree.
    
- **Beta-Pruning:** In a **MAX** layer, if the algorithm finds a branch that is already better than a previously found option (a value of **beta**), it can prune the remaining branches of that subtree.
    

#### 4. Multi-Objective Heuristic Search

- **Vector-Valued Costs:** Extends the A* algorithm to problems where the path cost is not a single number but a **vector** with multiple criteria (e.g., [cost, time, risk]).
    
- **The Challenge:** A key difficulty is that you cannot simply compare two cost vectors to find the "smallest."
    
- **Non-Dominating Sets:** Introduces the concept of **Pareto dominance**. One vector dominates another if it is better in at least one dimension and not worse in any other. A set of non-dominated solutions represents the best possible trade-offs.
    
- **A* Adaptation:** The standard A* algorithm's open list must be modified to hold a set of non-dominated paths instead of just the single best path.
    

#### 5. Applications in Economics

- **Market Competition:** Game trees model strategic interactions between competing companies (e.g., pricing wars, product launches).
    
- **Behavioral Economics:** These models predict how rational agents will behave in strategic scenarios like negotiations or bargaining.
    
- **Macroeconomic Policy:** Multi-objective optimization is directly applicable to policy-making, such as a central bank balancing multiple objectives like **inflation**, **unemployment**, and **economic growth**. The cost vector in this case would represent these different outcomes.
    

The lecture concludes by setting the stage for the next topic, a shift toward data-driven models and machine learning, starting with unsupervised learning.