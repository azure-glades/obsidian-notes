**Adversarial Search** is a search problem where you aren't just looking for a path to a goal, but you are doing so while an **opponent** is actively trying to stop you or move the state toward their own goal.
### Key Characteristics
- **Multi-Agent:** There are at least two players (the Maximizer and the Minimizer).
- **Conflicting Goals:** Usually "Zero-Sum"—if I gain +1 point, you lose -1 point.
- **Turn-Based:** Players take turns, which creates the "layers" of the search tree.
- **Game Tree Representation:** The search space is a tree where each level represents a different player's turn.
# Game Trees
- **Thinking Process:** Model the game as a directed graph where nodes are "game states" and edges are "moves." Layers alternate between your turn and the opponent's turn.
- **Key Idea:** Represent every possible future move to determine the best current move.

>[!note] Key concepts
    > **Zero-Sum**: A game where one player's gain is exactly equal to the other player's loss ($Utility_{Max} + Utility_{Min} = 0$).
    > **Terminal State**: A state where the game ends (Win, Loss, or Draw).
    > **Utility Function**: A numeric value assigned to terminal states (e.g., +1 for win, -1 for loss).
# [[MiniMax Algorithm]]
- **Thinking Process:** Assume the opponent is playing perfectly. You choose moves that maximize your score (**MAX**), while the opponent chooses moves that minimize it (**MIN**).
- **Key Idea:** Back-propagate values from terminal leaves up to the root.
- **Simple Algorithm:**
    1. **If** state is a terminal leaf, return its utility value.
    2. **If** current level is **MAX**:
        - Return the maximum value of all child nodes.
    3. **If** current level is **MIN**:
        - Return the minimum value of all child nodes.
    > Optimal Strategy: Minimax provides the best possible move against an optimal opponent.
    > Complexity: $O(b^m)$, where $b$ is the branching factor and $m$ is the maximum depth. This is often too slow for complex games.
# [[AlphaBeta Algorithm]] - Pruning
- **Thinking Process:** Why search a branch if you already know it's worse than a path you've already found? "Prune" the branches that cannot possibly influence the final decision.
- **Key Idea:** Maintain two values, $\alpha$ (the best score MAX is guaranteed) and $\beta$ (the best score MIN is guaranteed).
- **Simple Algorithm:**
    1. Initialize $\alpha = -\infty$ and $\beta = +\infty$.
    2. **MAX** updates $\alpha$: If a child returns a value $\geq \beta$, stop searching other children (Prune).
    3. **MIN** updates $\beta$: If a child returns a value $\leq \alpha$, stop searching other children (Prune).

>[!important]
    > $\alpha$ (Alpha): The best (highest) value found so far along the path for MAX.
    > $\beta$ (Beta): The best (lowest) value found so far along the path for MIN.
    > Pruning Condition: Stop searching a branch as soon as $\beta \leq \alpha$.
# Practical Heuristics (Evaluation Functions)
- **Thinking Process:** In real games (like Chess), the tree is too deep to reach terminal leaves. We must stop at a "cutoff" depth and _guess_ who is winning.
- **Key Idea:** Replace the terminal utility with an **Evaluation Function** $E(s)$ that estimates the state's value.
- **Key Concepts:**
    > Heuristic Alpha-Beta: Uses $f(s, d) = \text{EVAL}(s)$ when a search depth $d$ is reached instead of waiting for a game-over state.
    > **Quiescence Search:** Expanding "unstable" positions (like a piece being captured) beyond the depth limit to prevent the "horizon effect."
