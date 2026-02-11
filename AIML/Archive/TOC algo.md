That's a very common and important set of questions in the Theory of Computation. For an exam, you should focus on the _core idea_ of each algorithm.

Here are the decision properties algorithms explained in simple, vague terms:

---

## 1. Emptiness ($L(G) = \emptyset$?)

**Question:** Does the grammar $G$ generate **any** string at all?

### The Core Idea: The Generating Variables

The algorithm checks if the starting symbol ($S$) can eventually derive (or "lead to") a string of only terminal symbols (the actual letters/words). We don't care _which_ string, only _if_ a string is possible.

### Simple Vague Algorithm:

1. **Mark the Building Blocks:** Start by marking all **terminal symbols** (the 'letters' or final words) as "Good" or "Generating."
    
2. **Propagate the Goodness:** Repeat the following step until no new symbols can be marked:
    
    - Look at every grammar rule ($A \to X Y Z...$)
        
    - If **all** the symbols on the right-hand side ($X Y Z...$) are **already marked** as "Good," then mark the variable on the left-hand side ($A$) as "Good" too.
        
3. **Check the Start:**
    
    - If the **Start Symbol ($S$)** is marked as "Good," the language **is NOT empty** (it can generate a string).
        
    - If the **Start Symbol ($S$)** is **not** marked, the language **IS empty**.
        

## 2. Finiteness ($|L(G)|$ is finite?)

**Question:** Does the grammar $G$ generate only a **limited** (finite) number of distinct strings, or can it generate an **infinite** number of strings?

### The Core Idea: Detecting Cycles/Loops

A language is infinite if and only if there's a way for a variable to derive itself _and_ the part of the derivation that creates the loop can produce a real terminal string. In simple terms, we are looking for a usable **loop** that allows for endless repetition.

### Simple Vague Algorithm:

1. **Clean the Grammar (Preparation):** First, simplify the grammar by removing all "useless" parts (variables that can't generate a terminal string, or those that can't be reached from the start symbol). This is crucial.
    
2. **Draw the Dependency Graph:** Create a graph where each **variable** (non-terminal) is a node. Draw an edge from variable $A$ to variable $B$ if the grammar has a rule $A \to \dots B \dots$ (meaning $A$ can directly lead to $B$).
    
3. **Check for Cycles/Loops:**
    
    - Search the graph for any **cycle** (a path from a variable back to itself).
        
    - If a variable reachable from the start symbol is part of a cycle, it means that variable can be repeated infinitely, making the language **INFINITE**.
        
    - If no such cycle exists, every derivation must eventually end, and the language is **FINITE**.
        

## 3. Membership ($w \in L(G)$?)

**Question:** Given a specific string $w$ (e.g., "aabb"), can the grammar $G$ generate **exactly** that string?

### The Core Idea: Dynamic Programming / Table Filling (The CYK Algorithm)

The standard and most robust method is the **CYK Algorithm** (Cocke–Younger–Kasami). This algorithm checks every possible way to combine substrings to see if they can form the target string, working from small substrings up to the full string.

### Simple Vague Algorithm:

1. **Pre-Process:** Ensure the grammar is in a simple, standardized form (usually **Chomsky Normal Form, CNF**), where rules are only $A \to B C$ or $A \to a$.
    
2. **Build a Table (Bottom-Up):** Create a triangular table where the bottom row represents all substrings of length 1, the row above it all substrings of length 2, and so on, until the top cell represents the entire target string $w$.
    
3. **Fill the Table:**
    
    - **Length 1 (Bottom Row):** For each character in the string, list all the variables that can directly produce that character (e.g., if the character is 'a', and you have a rule $A \to a$, write 'A' in the cell).
        
    - **Longer Lengths (Working Upwards):** For a substring of length $N$, check all possible ways to split it into two smaller, adjacent substrings (length $k$ and length $N-k$).
        
    - **Combine and Check Rules:** For every pair of variables ($B$ and $C$) found in the cells for the two smaller substrings, check if the grammar has a rule $A \to B C$. If it does, add $A$ to the current cell.
        
4. **Final Check:**
    
    - If the **Start Symbol ($S$)** is present in the single, top-most cell (the one representing the entire string $w$), the string **IS a member** of the language.
        
    - Otherwise, it is not.

