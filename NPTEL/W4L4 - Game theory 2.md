### Game Theory: Mixed Strategy Nash Equilibrium

This lecture introduces the concept of **mixed strategies** to solve games that lack a **pure strategy Nash equilibrium**, using the penalty kick game as a primary example.

---

### 1. The Concept of Mixed Strategy

* **Pure Strategy:** "An action." A player chooses a single, specific action from their set of possibilities with certainty.
* **Mixed Strategy:** "A probability distribution over the set of actions of the player." Instead of choosing a single action, a player chooses a probability distribution, and then randomizes their choice based on that distribution.
    * For a set of actions $A = \{A_1, A_2, \dots, A_n\}$, a mixed strategy is a vector of probabilities $\{p_1, p_2, \dots, p_n\}$ where $\sum p_i = 1$.
    * A player chooses action $A_j$ with probability $p_j$.
    * A pure strategy is a special case of a mixed strategy where one probability is 1 and the rest are 0.

---

### 2. The Penalty Kick Game Revisited

The lecture revisits the penalty kick game from the previous session, which had **no pure strategy Nash equilibrium**.

* **Players:** Striker and Goalkeeper.
* **Actions:**
    * Striker: Kick Left (KL), Kick Right (KR).
    * Goalkeeper: Dive Left (DL), Dive Right (DR).
* **Payoff Matrix (Striker, Goalkeeper):**
    * (KL, DL): (0, 0)
    * (KL, DR): (V, -V)
    * (KR, DL): (1, -1)
    * (KR, DR): (0, 0)
    * *Note: V is a fraction less than 1, representing the probability of the striker scoring when kicking to their non-dominant side.*
* **The Goal:** Find a **mixed strategy Nash equilibrium**.

---

### 3. Finding the Mixed Strategy Nash Equilibrium

A mixed strategy Nash equilibrium exists if both players are indifferent between their available pure strategies, given that the other player is playing their equilibrium mixed strategy. This indifference is the condition that makes a player willing to randomize.

#### **Striker's Perspective (Finding the Goalkeeper's Mixed Strategy)**

The Striker will be indifferent between kicking left and kicking right only if the **expected payoffs** from both actions are equal.

* **Goalkeeper's Mixed Strategy:** Dive Left with probability **Q**, Dive Right with probability **(1 - Q)**.
* **Striker's Expected Payoff from KL:** (Payoff if GK dives L) $\times$ (Prob of GK diving L) + (Payoff if GK dives R) $\times$ (Prob of GK diving R)
    * $E_{striker}(KL) = 0 \times Q + V \times (1 - Q) = V(1 - Q)$
* **Striker's Expected Payoff from KR:**
    * $E_{striker}(KR) = 1 \times Q + 0 \times (1 - Q) = Q$
* **Condition for Indifference:** $E_{striker}(KL) = E_{striker}(KR)$
    * $V(1 - Q) = Q$
    * $V - VQ = Q$
    * $V = Q(1 + V)$
    * $Q = \frac{V}{1 + V}$

* **Conclusion:** The Striker will only play a mixed strategy (P > 0) if the Goalkeeper plays a mixed strategy where $Q = \frac{V}{1 + V}$.

#### **Goalkeeper's Perspective (Finding the Striker's Mixed Strategy)**

Similarly, the Goalkeeper will be indifferent between diving left and diving right only if the expected payoffs from both actions are equal.

* **Striker's Mixed Strategy:** Kick Left with probability **P**, Kick Right with probability **(1 - P)**.
* **Goalkeeper's Expected Payoff from DL:** (Payoff if Striker kicks L) $\times$ (Prob of Striker kicking L) + (Payoff if Striker kicks R) $\times$ (Prob of Striker kicking R)
    * $E_{goalkeeper}(DL) = 0 \times P + (-1) \times (1 - P) = -(1 - P)$
* **Goalkeeper's Expected Payoff from DR:**
    * $E_{goalkeeper}(DR) = (-V) \times P + 0 \times (1 - P) = -VP$
* **Condition for Indifference:** $E_{goalkeeper}(DL) = E_{goalkeeper}(DR)$
    * $-(1 - P) = -VP$
    * $1 - P = VP$
    * $1 = P(1 + V)$
    * $P = \frac{1}{1 + V}$

* **Conclusion:** The Goalkeeper will only play a mixed strategy (Q > 0) if the Striker plays a mixed strategy where $P = \frac{1}{1 + V}$.

---

### 4. The Mixed Strategy Nash Equilibrium

A mixed strategy Nash equilibrium is found when both players are willing to randomize simultaneously. This occurs when the indifference conditions for both players are met.

* **Striker's Equilibrium Strategy (P):** $P = \frac{1}{1 + V}$
* **Goalkeeper's Equilibrium Strategy (Q):** $Q = \frac{V}{1 + V}$

This equilibrium is stable because if the Striker plays with probability P = $\frac{1}{1+V}$, the Goalkeeper is indifferent and has no incentive to deviate from playing with probability Q = $\frac{V}{1+V}$. Symmetrically, if the Goalkeeper plays with probability Q = $\frac{V}{1+V}$, the Striker is indifferent and has no incentive to deviate from playing with probability P = $\frac{1}{1+V}$.

The next lecture will introduce the concept of simultaneous move games with incomplete information, or Bayesian games, and will also inspect for mixed strategy Nash equilibrium.