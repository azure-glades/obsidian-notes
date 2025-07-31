This video, the ninth lecture in the NPTEL course "Artificial Intelligence for Economics," delivered by Addoi Mitro, an Assistant Professor at the Indian Institute of Technology, Kharagpur, builds upon previous discussions of heuristic search algorithms, particularly the A* algorithm. The core of this lecture extends these concepts to **multi-objective heuristic search** and introduces the crucial idea of **game trees**.

---

### Essential Topics and Key Points:

The lecture can be broken down into the following key topics:

#### 1. Introduction to Game Trees

- **Definition:** A game tree is a graphical representation of a sequential game, where each **node** represents a state of the system (e.g., a chess board configuration), and **edges** represent possible moves. It's structured in layers, with turns alternating between players.
    
- **Sequential Play:** Games like chess or tic-tac-toe involve players taking turns.
    
- **Opposing Objectives:** Players have opposing goals (e.g., in chess, one player's win means the other's loss). A state favorable to one player is unfavorable to the other.
    
- **Heuristic Values:** Each node in the tree is associated with a heuristic value, which estimates how "good" or "bad" that state is for a particular player relative to their goal.
    
- **Player Objectives (Convention):**
    
    - **Player P1 (Minimizer):** Aims to minimize the heuristic function (reach states with low values, indicating a favorable outcome for P1).
        
    - **Player P2 (Maximizer):** Aims to maximize the heuristic function (reach states with high values, indicating a favorable outcome for P2).
        
- **Game End (Leaf Nodes):** The game progresses until a "leaf node" is reached, signifying the end of the game where no further moves are possible. These leaf nodes have a final "value function" indicating the outcome for P1 (lower value = better for P1).
    
 
---

#### 2. Minimax Algorithm for Optimal Path Identification

- **Problem:** Initial heuristic functions are just estimates; players need to make optimal decisions to guarantee the best possible outcome.
    
- **Minimax Principle:** This algorithm works by recursively calculating the optimal heuristic values for each node in the game tree, starting from the leaf nodes and working upwards.
    
    - **Maximizer's Turn (P2):** At nodes where P2 is to move, P2 will choose the move that leads to the child node with the _maximum_ heuristic value. This maximum value is then assigned as the heuristic for the current node.
        
    - **Minimizer's Turn (P1):** At nodes where P1 is to move, P1 will choose the move that leads to the child node with the _minimum_ heuristic value. This minimum value is then assigned as the heuristic for the current node.
        
- **Optimal Path:** Once the minimax values are calculated for all nodes, players can follow the path that consistently leads to their optimal outcome, assuming the opponent also plays optimally.
    

---

#### 3. Alpha-Beta Pruning

- **Efficiency Improvement:** Minimax can be computationally expensive as it evaluates the entire game tree. Alpha-Beta Pruning is an optimization that avoids evaluating parts of the tree that are irrelevant to the final decision.
    
- **Alpha Pruning (Minimizer's Turn):** If a minimizer (P1) finds a move that results in a value that is already lower than or equal to a previously found "alpha" value (the best option found so far for the maximizer at a higher level), then the rest of the minimizer's options from that node don't need to be explored. This is because the maximizer will never allow the game to reach these branches anyway.
    
- **Beta Pruning (Maximizer's Turn):** If a maximizer (P2) finds a move that results in a value that is already higher than or equal to a previously found "beta" value (the best option found so far for the minimizer at a higher level), then the rest of the maximizer's options from that node don't need to be explored. This is because the minimizer will never allow the game to reach these branches anyway.
    
- **Result:** Pruning significantly reduces the number of nodes that need to be evaluated, making the search more efficient.
    

---

#### 4. Multi-Objective Heuristic Search

- **Vector-Valued Costs:** Unlike single-objective search (like finding the shortest path where cost is a single number), multi-objective search deals with situations where the path cost is a **vector** (e.g., [time, money, risk]).
    
- **Vector-Valued Heuristics:** Consequently, heuristic functions and f-values (g + h) also become vector-valued.
    
- **Challenge of Comparison:** The main challenge is that comparing vectors is not straightforward. One vector might be "better" in some dimensions but "worse" in others (e.g., [3,4,8] vs. [2,5,7]).
    
- **Non-Dominating Set:** When comparing vector-valued f-values, instead of a single "best" value, you might end up with a **non-dominating set** (also known as a Pareto front). A vector `A` dominates `B` if `A` is better than or equal to `B` in all dimensions and strictly better in at least one. If neither `A` dominates `B` nor `B` dominates `A`, they are non-dominating.
    
- __A_ Algorithm Adaptation:_* The standard A* algorithm's mechanism of selecting the single lowest f-value from the open list needs to be adapted. In multi-objective A*, you cannot simply close a vertex if its f-value is part of a non-dominating set; all non-dominated paths must be explored.
    
- **Guaranteed Outcome:** The algorithm guarantees finding a **non-dominated path to the goal**, rather than a single shortest path.
    

---

#### 5. Multi-Objective Game Trees

- **Extension of Concepts:** The principles of multi-objective heuristic search can be applied to game trees.
    
- **Vector-Valued Outcomes:** Leaf nodes and intermediate nodes in a multi-objective game tree would have vector-valued outcomes or heuristic values.
    
- **Player Decisions:** Players (minimizer and maximizer) would make decisions based on comparing these multi-dimensional vectors, aiming to choose options that are non-dominated for their objective.
    

---

#### 6. Relevance for Economics

- **Strategic Interactions:** Game trees are highly relevant for modeling strategic interactions among economic agents, such as:
    
    - **Competing Companies:** Companies making pricing, production, or marketing decisions in turn.
        
    - **Suppliers and Consumers:** Bargaining and negotiation scenarios.
        
- **Behavioral Economics:** Game trees provide a framework to predict the behavior of "rational agents" in various strategic situations (competition, bargaining, negotiations).
    
- **Macroeconomic Policy Making:** Multi-objective optimization is crucial for entities like central banks, which must consider multiple conflicting objectives (e.g., inflation, unemployment, economic growth) when formulating monetary policy.
    

---

The lecture concludes by setting the stage for the next lecture, which will shift focus to data-driven models and machine learning (specifically unsupervised learning) in economics.