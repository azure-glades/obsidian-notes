	### Rubenstein Bargaining: A Sequential Game of Negotiation

This lecture explores **Rubenstein bargaining**, a model for sequential bargaining, by building on the concepts of sequential games and **Subgame Perfect Nash Equilibrium (SPNE)**. The central insight is that a player's patience (or impatience) directly impacts their bargaining power and final payoff.

---

### 1. The Ultimatum Game: The Foundation

The lecture begins with a simple, one-shot bargaining scenario.
	
* **Game:** Player A offers a division of a prize worth 1, giving themselves $x_A$ and Player B $1-x_A$. Player B either accepts or rejects. If B rejects, both get 0.
* **Assumption:** B accepts if they are indifferent between accepting and rejecting.
* **SPNE:** By backward induction, Player B will accept any offer, no matter how small. Player A, knowing this, will make an offer of **(1, 0)**, keeping everything for themselves.
* **Conclusion:** In this one-shot game, the player who makes the offer holds all the bargaining power.

---

### 2. The Two-Period Rubenstein Bargaining Game

The model is extended to include a second period of negotiation.

* **Game:**
    * **Period 1:** Player A offers $(v_1, 1-v_1)$. Player B can accept or reject.
    * **Period 2:** If B rejects, a cost is incurred for waiting, represented by a **discount factor** $\delta$ (where $0 < \delta < 1$). B then makes a counter-offer $(v_2, 1-v_2)$. Player A can accept or reject.
* **Backward Induction:**
    1.  **End of the game (Period 2):** Player B offers $(v_2, 1-v_2)$. Player A will accept any offer where they get a non-negative payoff. Player B, knowing this, will offer $(1, 0)$ in terms of the second period's value, keeping everything for themselves. The payoff vector is $(\delta v_2, \delta (1-v_2))$, which becomes **(0, $\delta$)** for (A, B) after A accepts.
    2.  **Beginning of the game (Period 1):** Player A makes the initial offer. They know that if B rejects, B's payoff in the next period will be $\delta$. Therefore, A will offer B exactly $\delta$ to make them indifferent between accepting and rejecting. A keeps the rest.
* **SPNE:** The equilibrium offer is **($1-\delta$, $\delta$)**. Player A gets $1-\delta$ and Player B gets $\delta$.
* **Conclusion:** The ability to counter-offer significantly increases a player's payoff, from 0 to $\delta$.

---

### 3. The Infinitely Repeated Rubenstein Bargaining Game

The model is extended to allow for an infinite number of counter-offering periods.

* **Payoff Series:** The payoffs for the players would alternate as more periods are added:
    * **1-Period:** (1, 0)
    * **2-Periods:** ($1-\delta$, $\delta$)
    * **3-Periods:** ($1-\delta+\delta^2$, $\delta-\delta^2$)
* **SPNE with Infinite Periods:** By using a backward-looking geometric series or a more elegant method of setting the value of the game ($V^*$) equal to the value of its subgame, the equilibrium payoffs converge to a specific value.
    * Player 1's Payoff: $V^* = \frac{1}{1+\delta}$
    * Player 2's Payoff: $1-V^* = \frac{\delta}{1+\delta}$
* **Conclusion:** If both players know that they can keep negotiating forever, they will settle for this fair split immediately in the first period. The first player offers **($\frac{1}{1+\delta}$, $\frac{\delta}{1+\delta}$)**, and the second player accepts.

---

### 4. Asymmetric Discount Factors

The model is refined to account for different levels of patience between the two players.

* **Assumption:** Player 1 has a discount factor of $\delta_1$, and Player 2 has a discount factor of $\delta_2$ (where $0 < \delta_1, \delta_2 < 1$).
* **SPNE with Asymmetric Patience:** By applying the same logic as before, the equilibrium payoffs are found to be:
    * Player 1's Payoff: $$V^* = \frac{1-\delta_2}{1-\delta_1\delta_2}$$
    * Player 2's Payoff: $$1-V^* = \frac{\delta_2(1-\delta_1)}{1-\delta_1\delta_2}$$
* **Key Insights:**
    * **A player's payoff increases with their own discount factor.** A higher $\delta$ means you are more patient and value future payoffs more. This increases your bargaining power, leading to a better deal. $\frac{\partial V^*}{\partial \delta_1} > 0$.
    * **A player's payoff decreases with the other player's discount factor.** A more patient opponent has more bargaining power, which reduces your share of the deal. $\frac{\partial V^*}{\partial \delta_2} < 0$.
* **Final Conclusion:** Rubenstein bargaining demonstrates that **patience is a key source of bargaining power**. The more patient you are, the better your outcome will be. The more impatient your opponent is, the better your outcome will be.

# Whats the discount factor?
The **discount factor ($\delta$)** is a numerical value between 0 and 1 that represents how much a player values future payoffs relative to immediate payoffs. It's a key concept in dynamic games, especially in sequential bargaining models like the Rubenstein model.
Here's what it represents and why it's important:
### 1. The Value of Patience
* **Time Value of Money:** The core idea is that a reward received later is worth less than the same reward received today. A payoff of $100 today is more valuable than $100 a year from now because of factors like inflation and opportunity cost (what you could do with the money today).
* **Quantifying Patience:** The discount factor quantifies a player's patience.
    * A $\delta$ value closer to **1** means the player is **more patient**; they value future payoffs almost as much as current ones.
    * A $\delta$ value closer to **0** means the player is **less patient**; they heavily discount future payoffs and prefer an immediate resolution.
### 2. Its Role in Rubenstein Bargaining
In the Rubenstein bargaining model, the discount factor is what makes waiting to negotiate costly.
* **Cost of Delay:** If a player rejects an offer and the negotiation moves to the next period, the value of the prize is multiplied by the discount factor. For example, if a prize is worth 1 today, it's worth $\delta$ in the next period, and $\delta^2$ in the period after that.
* **Bargaining Power:** The discount factor is directly linked to a player's bargaining power. As the lecture demonstrated, a more patient player (with a higher $\delta$) has a better equilibrium payoff because they are more willing to wait for a better offer. Conversely, an impatient player (with a lower $\delta$) will get a smaller share of the prize because they're more eager to settle quickly.
* **First-Mover Advantage:** Even with an infinitely repeated game, a player who gets to make the first offer has an advantage, though this diminishes as players become infinitely patient (i.e., as $\delta$ approaches 1).

A discount factor helps to solve the problem of infinite payoffs in infinitely repeated games by turning the infinite sum of future payoffs into a finite geometric series, making the game mathematically tractable.

For a great overview of the concept, you might want to watch this video: [Game Theory 101: Discount Factors](https://www.youtube.com/watch?v=xZdSkOG2jW8).
http://googleusercontent.com/youtube_content/4