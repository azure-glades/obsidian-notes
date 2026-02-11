Alpha-Beta pruning is an optimization technique for the Minimax algorithm. It doesn't change the result of the search; it simply **stops exploring branches** that it knows cannot possibly affect the final decision.
### Thinking Process: The "Waste of Time" Logic
Imagine you are playing a game. You explore "Option A" and find it guarantees you a score of at least 10.
Now you start looking at "Option B." You see that if you take Option B, your opponent has a move that limits your score to 5.
You don't need to look at any other responses the opponent has for Option B. Whether their other moves give you 0, -10, or 2, you already know Option B is worse than Option A (which gave you 10). You **prune** the rest of the Option B branch.
### Key Concepts
> **$\alpha$ (Alpha):** The best value that the **Maximizer** is currently guaranteed to get at this level or higher. It starts at $-\infty$.
> **$\beta$ (Beta):** The best (lowest) value that the **Minimizer** is currently guaranteed to get at this level or higher. It starts at $+\infty$.
> **The Pruning Rule:** If at any point $\alpha \geq \beta$, the current player doesn't need to look any further. The opponent would have already forced a different path earlier in the tree.
### Pseudocode
This is the "classic" implementation. Notice how $\alpha$ and $\beta$ are passed down the tree and updated as we find better values.

``` al
ALGORITHM AlphaBeta(node, depth, alpha, beta, maximizingPlayer)
    IF depth = 0 or node is terminal then
        RETURN utility of node
	
    IF maximizingPlayer THEN
        value := −∞
        FOR each child of node DO
            value := max(value, ALPHABETA(child, depth − 1, alpha, beta, false))
            alpha := max(alpha, value)
            IF alpha ≥ beta THEN
                BREAK (* Beta cuToff *)
        RETURN value
	
    ELSE (* minimizing player *)
        value := +∞
        FOR each child of node do
            value := min(value, ALPHABETA(child, depth − 1, alpha, beta, true))
            beta := min(beta, value)
            IF beta ≤ alpha THEN
                BREAK (* Alpha cutoff *)
        RETURN value
```

### Why does this matter?
- **Search Depth:** In the best-case scenario (where you examine the best moves first), Alpha-Beta allows you to search **twice as deep** as standard Minimax in the same amount of time.
- **Complexity:** Standard Minimax is $O(b^m)$. With perfect move ordering, Alpha-Beta is $O(b^{m/2})$.
- **Move Ordering:** The algorithm is much more effective if you check "good" moves first. If you check the worst moves first, you might not prune anything at all.

| **Feature**       | **Minimax**         | **Alpha-Beta Pruning** |
| ----------------- | ------------------- | ---------------------- |
| **Final Result**  | Optimal move        | Same optimal move      |
| **Nodes Visited** | Every single node   | Only "relevant" nodes  |
| **Efficiency**    | $O(b^m)$            | Up to $O(b^{m/2})$     |
| **Requirement**   | Full tree traversal | Move ordering helps    |
