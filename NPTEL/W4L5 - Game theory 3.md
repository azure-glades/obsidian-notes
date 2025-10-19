### Game Theory: Incomplete Information and Bayesian Games

This lecture explores **simultaneous move games with incomplete information**, also known as **Bayesian games**. It builds on the core concepts of Nash Equilibrium by introducing uncertainty about other players' payoffs, strategies, and "types."

---

### 1. Games with Complete Information: A Review

The lecture starts with a familiar example of a two-player dating game with complete information, where all payoffs are common knowledge.

* **Scenario:** A boy and a girl must choose between going to a **Cricket match (C)** or a **Movie (M)** without communicating.
* **Payoff Matrix:** The first payoff is for the boy, the second for the girl

|        | Girl (C) | Girl (M) |
| ------ | -------- | -------- |
| Boy(C) | 10,5     | 0,0      |
| Boy(M) | 0,0      | 5,10     |

* **Nash Equilibria:** The game has two pure strategy Nash Equilibria: **(C, C)** and **(M, M)**. Both players are better off if they coordinate, but the payoffs differ depending on the location.
* **Mixed Strategy Nash Equilibrium:** The lecture also recalls that a mixed strategy Nash Equilibrium exists where the boy and girl randomize their choices with specific probabilities to make the other player indifferent.

---

### 2. Introducing Incomplete Information

* **Definition of Incomplete Information:** A game where at least one player does not know some key information about another player, such as their payoff function or what is most important to them.
* **The Boy-Girl Game with Incomplete Information:**
    * **New Scenario:** The boy is interested in meeting, but he is **uncertain about the girl's type**.
    * **Girl's Types:** The girl can be either **Interested (I)** or **Uninterested (U)** in meeting the boy.
    * **Payoffs by Type:**
        * **If Interested (I):** Her payoffs are as before (she prefers to be with the boy).
        * **If Uninterested (U):** Her payoffs are now reversed; she gets a positive payoff only if they **do not meet**, as she wants to avoid the boy. The boy's payoffs remain the same, as he is always interested in meeting her.

---

### 3. Key Concepts in Bayesian Games

* **Type:** A player's "type" encapsulates all of their private information that is relevant to the game, primarily their payoff function. In this game, the girl's type is either 'I' or 'U'.
* **Belief:** Since the boy doesn't know the girl's type, he forms a **belief**, which is a probability distribution over the set of her possible types.
    * In the lecture's example, the boy's belief is that the girl is **Interested with probability 1/2** and **Uninterested with probability 1/2**.
* **Common Knowledge of Beliefs:** The players' beliefs about each other are **common knowledge**, meaning everyone knows the beliefs, everyone knows that everyone knows, and so on.

---

### 4. Bayesian Nash Equilibrium (BNE)

* **Definition:** "A set of strategies, one for each type of each player, such that no type of any player has any incentive to change his or her strategy given the beliefs which are there about other players."
* **Core Principle:** A BNE is a Nash Equilibrium in a game of incomplete information. It requires each player to choose a strategy that is a best response to the other players' strategies, taking into account their beliefs about the other players' possible types.
* **Analysis of the Boy-Girl Game:**
    * **Step 1: The Boy's Expected Payoffs.** The boy's strategy must maximize his **expected payoff**, which is calculated by averaging his payoffs across the girl's possible types, weighted by his beliefs (1/2 for each type).
    * **Step 2: The Girl's Best Response.** The girl, who knows her own type, chooses a strategy that maximizes her payoff, given her belief about what the boy will do. The girl's strategy can be **type-dependent**.
    * **Result:** The lecture identifies a **pure strategy Bayes Nash Equilibrium**:
        * **Boy's Strategy:** Go to the **Cricket match (C)**. (This is his best response because his expected payoff is highest for this action).
        * **Girl's Strategy:** Go to the **Cricket match (C)** if she is **Interested**, and go to the **Movie (M)** if she is **Uninterested**. (These are her best responses, conditional on her own type).

This equilibrium is stable because, given this set of strategies, no player has a unilateral incentive to deviate. The boy plays his best response based on his beliefs, and the girl plays her best response based on her actual type.