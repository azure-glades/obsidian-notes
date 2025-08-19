### Game Theory: An Introduction to Strategic Interactions

This lecture provides an introduction to game theory, which is the study of strategic interactions between rational agents. The outcome for each agent depends on the actions of all others.

#### Core Concepts of Game Theory

* **Rationality of Players:** The assumption that every player selfishly maximizes their own objective or payoff, given the information available to them.
* **Common Knowledge:** "Any fact is said to be common knowledge if each player in the game or the system knows the fact, each player knows that every other player knows the fact, every player knows that every other player knows that every other player knows that particular fact and so on and so forth." This typically includes the rules, available actions, and payoffs of the game.

#### Types of Games

* **Simultaneous Move Games:** Players choose their actions at the same time without knowing what the other players are doing.
* **Sequential Move Games:** One player moves first, and the other players can observe that move before making their own.

#### Simultaneous Move Games: Complete Information

* **Structure:**
    * A set of players.
    * A set of possible actions for each player.
    * Players choose actions simultaneously, forming an **action profile**.
    * Each player has a payoff, typically represented in a **payoff matrix**, for each action profile.
* **Complete Information:** "A setting where each player has all information about the set of actions of all other players and the payoffs of all other players."

#### Key Concepts in Simultaneous Games

* **Action Profile:** "A couple of actions which have been chosen by all the players."
* **Nash Equilibrium (NE):** "An action profile is called a Nash equilibrium if no player has an incentive to do anything else given what the other players are doing." In a Nash Equilibrium, each player is playing their best response given the actions of the other players, and no player wants to unilaterally deviate.
* **Pure Strategy:** "An action." A pure strategy Nash equilibrium is one where each player chooses a single, specific action with certainty.

#### Example 1: The Go-Wait Game

* **Players:** Red car and Yellow car.
* **Actions:** Go, Wait.
* **Payoff Matrix:**
    * Wait, Wait: (0, 0)
    * Wait, Go: (0, 2)
    * Go, Wait: (2, 0)
    * Go, Go: (-10, -10)
* **Nash Equilibria:** This game has **two pure strategy Nash equilibria**:
    1.  **(Go, Wait):** If Red chooses Go, Yellow's best response is Wait (payoff 0 > -10). If Yellow chooses Wait, Red's best response is Go (payoff 2 > 0). Neither player has an incentive to deviate.
    2.  **(Wait, Go):** The symmetric opposite case, where neither player has an incentive to deviate.

#### Example 2: The Prisoner's Dilemma

* **Players:** Two prisoners (A and B).
* **Actions:** Cooperate (don't confess), Defect (confess).
* **Payoff Matrix (Years in Jail):**
    * Cooperate, Cooperate: (1, 1) - Best for society.
    * Defect, Cooperate: (0, 10)
    * Cooperate, Defect: (10, 0)
    * Defect, Defect: (5, 5) - Worst for both prisoners together.
* **Best Response Analysis:**
    * No matter what Prisoner A does, Prisoner B's best response is always to **Defect** (5 years is better than 10 years, and 0 years is better than 1 year).
    * Since Prisoner B will always Defect, Prisoner A's best response is also to **Defect** (5 years is better than 10 years).
* **Nash Equilibrium:** The **unique Nash equilibrium is (Defect, Defect)**.
* **Key Insight:** The Nash equilibrium outcome (5, 5) is not the most desirable outcome for the players. The outcome (1, 1), where both players cooperate, is **Pareto-dominant**, but it cannot be sustained because each player has a selfish incentive to deviate.

#### Example 3: The Penalty Kick Game

* **Players:** A striker and a goalkeeper.
* **Actions:**
    * Striker: Kick Left (KL), Kick Right (KR).
    * Goalkeeper: Dive Left (DL), Dive Right (DR).
* **Payoff Matrix (Striker, Goalkeeper):**
    * KL, DL: (0, 0)
    * KR, DL: (1, -1)
    * KL, DR: (V, -V)
    * KR, DR: (0, 0)
* **Best Response Analysis:**
    * Striker KL -> Goalkeeper's best response is DL (payoff 0 > -V).
    * Striker KR -> Goalkeeper's best response is DR (payoff 0 > -1).
    * Goalkeeper DL -> Striker's best response is KR (payoff 1 > 0).
    * Goalkeeper DR -> Striker's best response is KL (payoff V > 0).
* **Conclusion:** There is **no pure strategy Nash equilibrium**. Each player's best response depends entirely on what the other player does, leading to a continuous cycle of outguessing. This suggests that players may need to resort to randomizing their actions.

#### What's Next?
The lecture ends by foreshadowing the concept of **mixed strategies**, where players choose their actions randomly based on a probability distribution. This will be explored in the next lecture to find a potential Nash equilibrium for games like the Penalty Kick game.