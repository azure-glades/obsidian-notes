To understand the **Minimax** algorithm, you have to think of it as a recursive "look-ahead" strategy. You are trying to see into the future, assuming that both you and your opponent will play perfectly.
### Thinking Process: The Recursive Logic
Imagine you are at the root of a tree. You can't see the value of your current position until you look at the results of your possible moves.
1. **Down to the Leaves:** You "teleport" your brain to the end of the game (the terminal states).
2. **Assign Value:** At the end, you see a score (e.g., +10 for a win, -10 for a loss).
3. **Bubble Up:**
	* If it's your turn (**MAX**), you choose the move that leads to the highest score.
    - If it's the opponent's turn (**MIN**), you must assume they are smart enough to choose the move that leads to the lowest score for you.    

> **Recursive Backtracking:** The value of a parent node is determined only after the values of its children are calculated. It is a "bottom-up" evaluation.
> **Perfect Information:** Minimax assumes you can see the entire state space (like Chess or Go), not games with hidden info (like Poker).
### Pseudocode

This pseudocode follows a standard recursive structure. It uses a `depth` parameter to limit how far the "AI" looks ahead and a `is_maximizing` boolean to toggle between the two players.

``` al
ALGO minimax(state, depth, is_maximizing):
    // Base case: game over or reached search limit
    IF depth == 0 OR game_over(state):
        RETURN evaluate(state)
    
    IF is_maximizing:
        best_score = -infinity
        FOR move in get_legal_moves(state):
            # Recurse for the opponent (who is MIN)
            score = minimax(apply_move(state, move), depth - 1, False)
            best_score = max(best_score, score)
        RETURN best_score
        
    ELSE: // Minimizing player's turn
        best_score = infinity
        FOR move in get_legal_moves(state):
            // Recurse for the player (who is MAX)
            score = minimax(apply_move(state, move), depth - 1, True)
            best_score = min(best_score, score)
        RETURN best_score
```

| **Component**          | **Purpose**                                                                                                   |
| ---------------------- | ------------------------------------------------------------------------------------------------------------- |
| **`evaluate(state)`**  | The "Heuristic Function." If the game isn't over, it guesses who is winning (e.g., counting pieces in Chess). |
| **`depth`**            | Prevents the algorithm from searching forever. As depth increases, the AI becomes "smarter" but slower.       |
| **`max()` vs `min()`** | This represents the core conflict. **MAX** wants to increase the value; **MIN** wants to decrease it.         |
### The "Game Theory" Assumption
Minimax is **pessimistic**. It doesn't assume the opponent will make a mistake. Even if a move has a potential +100 reward, if the opponent has a response that leads to -50, Minimax will value that move as -50. It chooses the "best of the worst-case scenarios.