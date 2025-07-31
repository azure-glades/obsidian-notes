This lecture, "Artificial Intelligence for Economics - Lecture 8," delivered by Assistant Professor Adyay Mithro from IIT Kharagpur, shifts focus from optimization techniques to **heuristic search** within the domain of AI for economics.
### Gist of the Lecture

The lecture introduces the concept of **heuristic search** as a solution for sequential decision-making problems, particularly when the entire problem space (represented as a graph) is not fully known beforehand. Unlike traditional optimization or graph algorithms that require complete information, heuristic search algorithms use estimated "guesses" (heuristics) to navigate towards a goal state, making them suitable for real-world scenarios in economics where decisions are made step-by-step with incomplete information.

### Vital Topics and Key Points Discussed

#### 1. Optimization vs. Heuristic Search

- **Optimization (Previous Lectures):** Focused on resource allocation problems aiming to optimize an outcome under restrictions. These often assume a complete understanding of the problem space.
    
- **Heuristic Search (Current Lecture):** Addresses sequential problems where the "state of the system" evolves. The goal is to reach a desired state from an initial state by making step-by-step perturbations. This is crucial when the full graph of possible states and transitions isn't known upfront
#### 2. Graph Theory Fundamentals for Search

- **States as Vertices:** Each state of the system (e.g., resource allocation, game position) is represented as a **vertex** (or node) in a graph.
    
- **Transitions as Edges:** Possible changes or moves from one state to another are represented by **edges** connecting vertices.
    
- **Directed vs. Undirected Graphs:**
    
    - **Directed Graphs:** Edges have a specific direction (e.g., from A to B, but not necessarily B to A).
        
    - **Undirected Graphs:** Edges allow movement in both directions.
        
- **Path:** A sequence of connected edges in a graph, representing a series of steps to move from one state to another.
    
- **Connected Graph:** A graph where a path exists between every pair of vertices.
    
- **Graph Search Problem:** Starting at a root node and exploring other vertices by following edges, often to find specific target vertices.
    

#### 3. Weighted Graphs and Shortest Path Algorithms

- **Weighted Graph:** A graph where each edge has a numerical **weight** (or cost) associated with it, representing the cost of traversing that edge.
    
- **Path Weight:** The sum of the weights of all edges in a path.
    
- **Shortest Path Problem:** Finding the sequence of moves (path) between a source and a target vertex that has the minimum total weight.
    
- **Traditional Shortest Path Algorithms (when the entire graph is known):**
    
    - **Dijkstra's Algorithm**
        
    - **Floyd-Warshall Algorithm**
        
    - These are "provably correct" and converge to the exact solution when full graph information is available.
        

#### 4. The Need for Heuristic Search

- **Limitations of Traditional Algorithms:** They fail when the "entire graph along with all the vertices and edges and their weights are not known beforehand."
    
- **Progressive Revelation:** In many real-world scenarios (like chess or economic decision-making), new states and transitions are revealed only as one traverses the graph.
    
- **Examples:**
    
    - **Game of Chess:** Each board configuration is a state; moves are transitions. The full game tree is too vast to know in advance.
        
    - **Resource Allocation in Economics:** Changing allocations from one sector to another.
        
    - **COVID-19 Decision Making:** Imposing lockdowns or not, with immediate consequences known but long-term outcomes uncertain.
        
    - **Supply Chain Optimization:** Companies needing to minimize costs or maximize efficiency without a complete view of all uncertainties.
        
    - **Portfolio Optimization:** Sequential investment decisions where future asset behavior isn't fully predictable.
        

#### 5. Heuristic Search Technique

- **Heuristic Function (h(x)):** An **estimate** of how "far" a given state `x` is from a goal state. It's a "guess" and may not be the true value.
    
- **Total Estimated Cost (f(x)):** For any given state `x` on a path from the start to a goal, `f(x) = g(x) + h(x)`.
    
    - **g(x):** The **actual cost** of going from the **start vertex** to the **current node x**.
        
    - **h(x):** The **projected (estimated) cost** of going from the **current vertex x** to one of the **goal nodes**.
        

#### 6. A* Algorithm

- **Best-First Search:** The A* algorithm is a type of best-first search. At each step, it explores the option that appears "best" based on its `f(x)` value (lowest estimated total cost).
    
- **Mechanism:**
    
    1. Start at the initial node (A in the example).
        
    2. Identify neighbors and add them to an "open list" (nodes to visit).
        
    3. Calculate `f(x)` for each neighbor using `g(x)` (known cost from start) and `h(x)` (heuristic estimate).
        
    4. Select the node from the open list with the lowest `f(x)` value to explore next.
        
    5. Move to that node, add it to the "closed list" (visited nodes), and repeat the process with its neighbors.
        
    6. Stop when a goal node is reached.
        
- **Admissibility of Heuristic:**
    
    - For A* to guarantee finding the **shortest path**, the heuristic function `h(x)` must be **admissible**.
        
    - **Admissible Heuristic:** Always **underestimates** (or is equal to) the true least cost to any goal state.
        
    - **Consequence of Overestimation:** If `h(x)` overestimates the true cost, A* is **not guaranteed** to find the shortest path, as demonstrated by an example where a longer path was chosen due to a misleading heuristic value.
        
    - **Simple Admissible Choice:** A safe choice for `h(x)` is to take the minimum cost to any of its direct neighbors, as this will always underestimate the total cost to the goal.
        


The lecture concludes by emphasizing the practical importance of heuristic search in various economic applications where decisions are made

[[W2L4 - Heuristics and Game Trees]]