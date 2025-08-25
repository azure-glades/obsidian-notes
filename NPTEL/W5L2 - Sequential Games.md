### Sequential Games: Modeling Strategic Interactions Over Time

This lecture shifts from simultaneous move games to **sequential games**, where players make decisions in a specific order, and later players can observe the actions of earlier players. The key tool for solving these games is **backward induction**.

---

### 1. Introduction to Sequential Games

* **Core Idea:** In sequential games, players move one after another. A later player's action is a response to an earlier player's observable action.
* **Backward Induction:** "A process of reasoning backwards in time from the end of a problem or situation and determine the sequence of optimal actions." This is the primary method for solving sequential games. It involves starting at the final decision point and working backward to the beginning.
* **Pirate Gold Coin Puzzle:** This puzzle is used to illustrate the power of backward induction. By analyzing the optimal outcomes at the end of the game (when only a few pirates are left), one can determine the optimal proposal for the senior-most pirate at the beginning.
    * **Result:** The most senior pirate (A) needs only 3 votes (himself + 2 others) to pass his proposal. He can secure these votes by offering just one gold coin each to pirates C and E, who would otherwise get nothing if he were killed. His optimal proposal is **(98, 0, 1, 0, 1)**, keeping 98 coins for himself.

---

### 2. Formal Definitions of Sequential Games

* **Extensive Form Game:** A sequential game is also known as an extensive form game.
* **Key Features:**
    1.  **Set of Players:** The agents involved in the game.
    2.  **Histories:** "A sequence of actions chosen by different players." A **terminal history** is a sequence of actions after which the game ends.
    3.  **Player Function:** A function that assigns a player to each history, indicating whose turn it is to move.
    4.  **Payoff:** A payoff for each player is associated with every terminal history.
* **Strategy:** "A function that assigns to each history an action chosen from the set of actions which player i can choose." A strategy in a sequential game is a complete plan of action that specifies what a player will do at every point in the game where it is their turn to move.

---

### 3. Solving Sequential Games with Backward Induction

The core idea is to find the **Subgame Perfect Nash Equilibrium (SPNE)** by working backward from the end of the game tree.

#### Example 1: Entrant vs. Incumbent
* **Players:** Entrant and Incumbent.
* **Game Flow:**
    1.  The Entrant moves first: `In` or `Out`.
    2.  If the Entrant chooses `Out`, the game ends.
    3.  If the Entrant chooses `In`, the Incumbent observes this and chooses to `Accommodate` or `Fight`.
* **Payoffs:**
    * `(Out)`: (0, 10)
    * `(In, Fight)`: (-5, -5)
    * `(In, Accommodate)`: (5, 5)
* **Backward Induction Analysis:**
    1.  **Start at the end:** The Incumbent's decision point. If the Entrant has chosen `In`, the Incumbent must choose between `Accommodate` (payoff 5) and `Fight` (payoff -5). The optimal choice is to **accommodate**.
    2.  **Move back:** The Entrant's decision point. The Entrant now knows the Incumbent's optimal response.
        * If the Entrant chooses `Out`, their payoff is 0.
        * If the Entrant chooses `In`, the Incumbent will accommodate, and the Entrant's payoff is 5.
    3.  **Optimal Strategy:** The Entrant's optimal choice is to choose **In**.
* **Subgame Perfect Nash Equilibrium (SPNE):** The SPNE is the action profile where the Entrant chooses `In`, and the Incumbent chooses `Accommodate`. This is an SPNE because every player's strategy is optimal in every possible subgame.

#### Example 2: The Two-Player Game
* **Game Flow:** Player 1 chooses `L` or `R`. Then Player 2 chooses `U` or `D`. If Player 1 chose `L` and Player 2 chose `U`, Player 1 moves again.
* **Backward Induction Analysis:**
    1.  **Last decision point:** Player 1's second move. The payoffs are (3, 2) for `L` and (6, 10) for `R`. Player 1's optimal choice is **`R`** (payoff 6 > 3).
    2.  **Player 2's decision points:**
        * At the `L` branch, Player 2 knows Player 1 will choose `R` next, giving Player 2 a payoff of 10. If Player 2 chose `D`, their payoff would have been 5. The optimal choice is **`U`** (payoff 10 > 5).
        * At the `R` branch, Player 2 chooses between `U` (payoff 2) and `D` (payoff 10). The optimal choice is **`D`**.
    3.  **Player 1's first decision point:** Player 1 now knows the optimal sequence of moves for each of their initial choices.
        * If Player 1 chooses `L`, the game path will be `L -> U -> R`, and Player 1's final payoff will be 6.
        * If Player 1 chooses `R`, the game path will be `R -> D`, and Player 1's final payoff will be 5.
    4.  **Optimal Strategy:** Player 1 will choose **`L`** to get a higher payoff.
* **SPNE:** The SPNE is the strategy where Player 1's initial move is `L`, Player 2's move is `U` (if Player 1 chose `L`), and Player 1's second move is `R` (if Player 2 chose `U`).

The next lecture will apply this concept of backward induction to the idea of bargaining.