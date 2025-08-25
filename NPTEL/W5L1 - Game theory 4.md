### Game Theory: Mixed Strategy Bayes Nash Equilibrium

This lecture continues the analysis of the dating game with incomplete information to find a **mixed strategy Bayes Nash Equilibrium (BNE)**. It extends the concept of mixed strategies to a setting where one player is uncertain about the other's "type."

---

### 1. Game Setup and Goal

* **Players:** A boy (1 type: Interested) and a girl (2 types: Interested or Uninterested).
* **Belief:** The boy believes the girl is **Interested with probability 1/2** and **Uninterested with probability 1/2**. This belief is common knowledge.
* **Goal:** Find a mixed strategy BNE, which is a set of strategies (one for each player type) where no type of any player has an incentive to deviate.

#### Strategies:
* **Boy:** Plays Cricket (C) with probability **p**, Movie (M) with probability **1-p**.
* **Interested Girl (Type I):** Plays C with probability **$q_1$**, M with probability **1-$q_1$**.
* **Uninterested Girl (Type U):** Plays C with probability **$q_2$**, M with probability **1-$q_2$**.

The goal is to find the values of p, $q_1$, and $q_2$ that constitute a mixed strategy BNE.

---

### 2. The Boy's Perspective: The Girl Connect Equation

The boy will only play a mixed strategy (i.e., choose a value of $p$ between 0 and 1) if he is **indifferent** between playing C and M. This means his expected payoff from playing C must equal his expected payoff from playing M.

* **Expected Payoff from C:**
    * $E_{boy}(C) = ( \text{Payoff if girl is I} \times P(\text{I}) ) + ( \text{Payoff if girl is U} \times P(\text{U}) )$
    * Payoff (I) = $10 \times q_1 + 0 \times (1-q_1) = 10q_1$
    * Payoff (U) = $10 \times q_2 + 0 \times (1-q_2) = 10q_2$
    * $E_{boy}(C) = \frac{1}{2}(10q_1) + \frac{1}{2}(10q_2) = 5(q_1 + q_2)$

* **Expected Payoff from M:**
    * Payoff (I) = $0 \times q_1 + 5 \times (1-q_1) = 5(1-q_1)$
    * Payoff (U) = $0 \times q_2 + 5 \times (1-q_2) = 5(1-q_2)$
    * $E_{boy}(M) = \frac{1}{2}(5(1-q_1)) + \frac{1}{2}(5(1-q_2)) = 2.5(1-q_1 + 1-q_2)$

* **Indifference Condition:** $E_{boy}(C) = E_{boy}(M)$
    * $5(q_1 + q_2) = 2.5(2 - q_1 - q_2)$
    * $2(q_1 + q_2) = 2 - q_1 - q_2$
    * $3(q_1 + q_2) = 2$
    * This is the "Girl Connect Equation" that must be satisfied for the boy to play a proper mixed strategy.

---

### 3. The Girl's Perspective: Finding Her Best Response

The girl knows the boy's strategy (p) and her own type. She will play a mixed strategy only if she is indifferent between C and M.

#### **Interested Girl's Indifference Condition:**
* **Expected Payoff from C:** $E_{Igirl}(C) = 5 \times p + 0 \times (1-p) = 5p$
* **Expected Payoff from M:** $E_{Igirl}(M) = 0 \times p + 10 \times (1-p) = 10(1-p)$
* **Indifference:** $5p = 10(1-p) \implies 15p = 10 \implies \mathbf{p = 2/3}$.
    * **Conclusion:** The Interested girl will only play a mixed strategy if the boy plays C with probability $p=2/3$.

#### **Uninterested Girl's Indifference Condition:**
* **Expected Payoff from C:** $E_{Ugirl}(C) = 0 \times p + 5 \times (1-p) = 5(1-p)$
* **Expected Payoff from M:** $E_{Ugirl}(M) = 10 \times p + 0 \times (1-p) = 10p$
* **Indifference:** $5(1-p) = 10p \implies 5 = 15p \implies \mathbf{p = 1/3}$.
    * **Conclusion:** The Uninterested girl will only play a mixed strategy if the boy plays C with probability $p=1/3$.

---

### 4. Finding the Mixed Strategy BNE

This analysis reveals two possible mixed strategy BNEs, depending on which type of girl's indifference condition is met.

#### **Bayes Nash Equilibrium 1 (Triggered by Interested Girl's Indifference):**
* **Boy's Strategy (p=2/3):** The boy plays C with probability **2/3** and M with probability **1/3**.
* **Girl's Strategies:**
    * **Interested Girl:** Since $p=2/3$, she is indifferent and can play a mixed strategy. The girl connect equation ($3(q_1 + q_2) = 2$) must hold.
    * **Uninterested Girl:** Since $p=2/3 > 1/3$, she is not indifferent. Her best response is to play the pure strategy that maximizes her payoff, which is to play **M** ($q_2=0$).
* **Solving for $q_1$:** Plug $q_2=0$ into the Girl Connect Equation: $3(q_1 + 0) = 2 \implies \mathbf{q_1 = 2/3}$.
* **Equilibrium 1 Strategies:**
    * **Boy:** (p=2/3, 1-p=1/3)
    * **Interested Girl:** ($q_1$=2/3, 1-$q_1$=1/3)
    * **Uninterested Girl:** ($q_2$=0, 1-$q_2$=1)

#### **Bayes Nash Equilibrium 2 (Triggered by Uninterested Girl's Indifference):**
* **Boy's Strategy (p=1/3):** The boy plays C with probability **1/3** and M with probability **2/3**.
* **Girl's Strategies:**
    * **Uninterested Girl:** Since $p=1/3$, she is indifferent and can play a mixed strategy. The girl connect equation must hold.
    * **Interested Girl:** Since $p=1/3 < 2/3$, her best response is to play the pure strategy that maximizes her payoff, which is to play **M** ($q_1=0$).
* **Solving for $q_2$:** Plug $q_1=0$ into the Girl Connect Equation: $3(0 + q_2) = 2 \implies \mathbf{q_2 = 2/3}$.
* **Equilibrium 2 Strategies:**
    * **Boy:** (p=1/3, 1-p=2/3)
    * **Interested Girl:** ($q_1$=0, 1-$q_1$=1)
    * **Uninterested Girl:** ($q_2$=2/3, 1-$q_2$=1/3)

These two mixed strategy profiles constitute the two mixed strategy Bayes Nash Equilibria for this game. They are stable because, in each case, no player has an incentive to deviate given the strategies of the others.