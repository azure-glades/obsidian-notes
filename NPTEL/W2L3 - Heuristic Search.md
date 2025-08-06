This lecture, "Artificial Intelligence for Economics - Lecture 8," delivered by Assistant Professor Adyay Mithro, shifts the focus from traditional optimization to **heuristic search techniques**, a class of sequential decision-making problems often modeled using graphs.

---

## Gist of the Video

The lecture explains how to solve problems where the entire problem space is not known in advance, such as in game theory or economic decision-making. Instead of knowing the full map, you only discover new possibilities (neighboring nodes) as you move. The core concept is using **graph search** algorithms, specifically the A* algorithm_, which employs a **heuristic function** to estimate the cost to the goal from any given state. This allows for a directed, "best-first" search that is more efficient than uninformed methods. The lecture emphasizes the importance of an **admissible heuristic** (one that never overestimates the true cost) to guarantee finding the optimal solution and highlights the practical applications of these techniques in economics, including resource allocation, macroeconomic policy, and portfolio optimization.

---

## Vital Topics and Key Points Discussed

### 1. The Problem: Sequential Decision-Making

- **Context:** Unlike traditional optimization where the entire problem is known upfront, here we face a sequential problem.
    
- **State:** The system is described by a "state" (e.g., a specific resource allocation or a game board configuration).
    
- **Goal:** The aim is to move from a starting state to a desired "goal state" by taking a series of steps.
    
- **Sequential Nature:** The key challenge is that the entire "graph" of all possible states and transitions is not known initially. New states are only revealed as the search progresses.
    

### 2. Graph Search Fundamentals

- **Graph:** A collection of **vertices** (states) and **edges** (transitions or moves).
    
- **Directed vs. Undirected Edges:** Edges can be one-way (directed, with an arrow) or two-way (undirected). This determines the possible paths.
    
- **Path:** A sequence of connected edges.
    
- **Weighted Graphs:** Edges have a numerical **weight** or **cost** associated with them. The cost of a path is the sum of its edge weights.
    
- **Shortest Path:** Finding the path with the minimum total weight between a source and a target vertex.
    
- **Traditional Algorithms:** Mentioned algorithms like **Dijkstra's** and **Floyd-Warshall's** are effective for finding shortest paths but require the **entire graph to be known in advance**.
    

### 3. Heuristic Search and the A* Algorithm

- **Heuristic Search:** A technique used when the entire graph is not known. It uses an estimate, or "guess," to guide the search.
    
- **Heuristic Function (h(x)):** An estimate of the cost to reach a goal state from the current vertex x.
    
- Evaluation Function (f(x)): The total estimated cost of a path from the start to the goal, passing through vertex x. It's defined as:
    
    f(x)=g(x)+h(x)
    
    - **g(x):** The actual cost of the path already traversed from the start vertex to the current vertex x.
        
    - **h(x):** The heuristic estimate of the cost from x to the goal.
        
- __A_ Algorithm (Best-First Search):_*
    
    - This is an informed search algorithm.
        
    - It maintains an `open` list of vertices to be explored.
        
    - In each step, it selects the vertex from the `open` list that has the **lowest f(x) value**. This is the "best-first" principle.
        
    - It then expands this vertex, adding its neighbors to the `open` list and updating their g and f values.
        
    - The search continues until a goal node is selected for expansion.
        

### 4. Admissibility and Optimality

- **The Problem:** Unlike Dijkstra's, A* is not guaranteed to find the shortest path unless a specific condition is met.
    
- **Admissible Heuristic:** A heuristic function h(x) is **admissible** if it **never overestimates** the true cost to the goal. That is, h(x)≤h∗(x) for all nodes x, where h∗(x) is the true shortest path cost.
    
- **Guaranteed Optimality:** If the heuristic function is admissible, the __A_ algorithm is guaranteed to find the shortest path_* to the goal.
    
- **Non-Admissible Heuristic:** The lecture demonstrates with an example where h(d)=10 even though the true cost from d to the goal is 3. This non-admissible heuristic causes A* to choose a suboptimal path (cost 9) and miss the true optimal path (cost 8).
    
- **Example Admissible Heuristic:** A simple admissible heuristic for a node is to take the **minimum cost to any of its direct neighbors**. This is a safe lower bound.
    

### 5. Applications in Economics

- **Navigating Decisions:** A* and heuristic search are relevant for making sequential decisions where the full consequences are unknown (e.g., in macroeconomic policy or in a firm's pricing strategy).
    
- **Supply Chain Optimization:** Companies can use these methods to optimize their supply chains to minimize costs or maximize efficiency, taking one decision at a time without knowing the entire future state of the supply chain.
    
- **Portfolio Optimization:** When making investment decisions, a sequential approach is necessary. A heuristic search can help navigate the complex space of investment choices without having perfect foresight.