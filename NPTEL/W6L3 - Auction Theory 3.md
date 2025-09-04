### The First-Price Auction: A Bayesian Game

This lecture continues the study of auctions by focusing on the **First-Price Auction** and its unique characteristics from a game-theoretic perspective. The main goal is to determine an optimal bidding strategy for a rational buyer in this type of auction.

---

### 1. First-Price Auction Setup

* **Scenario:** One seller, one object, and $N$ buyers.
* **Mechanism:**
    * All buyers submit simultaneous, sealed bids.
    * The buyer with the **highest bid wins** the object.
    * The winner pays their exact bid amount.
* **Game Theory:** A first-price auction induces a game among the bidders. The lecture notes that for a first-price auction, there is no Nash Equilibrium in a complete information strategic game. Therefore, the problem must be framed as a **Bayesian game**, where players have private information.

---

### 2. The Main Theorem and Assumptions

The lecture presents a key theorem for the first-price auction's optimal strategy under specific assumptions.

* **Theorem:** "In the Bayesian game induced by the first price auction, each buyer bidding half their valuations forms a Bayesian Nash equilibrium."
* **Assumptions for the Proof:**
    1.  There are only **two buyers**.
    2.  Each buyer's valuation ($\theta_i$) is distributed **uniformly randomly** in the interval [0, 1].
    3.  Each buyer is **risk-neutral**.

---

### 3. Risk Attitudes: A Brief Primer

The lecture briefly explains different attitudes toward risk using an example of two options: a guaranteed ₹100 vs. a 50% chance of ₹200 and a 50% chance of ₹0. Both options have an expected value of ₹100.

* **Risk-Seeking:** Prefers the second, more uncertain option.
* **Risk-Averse:** Prefers the first, guaranteed option.
* **Risk-Neutral:** Is indifferent between the two options. This is a key assumption for the theorem's proof.

---

### 4. Proof of the Theorem (for 2 Buyers)

The proof demonstrates that bidding half of one's valuation is a Bayesian Nash Equilibrium for two buyers under the given assumptions.

* **Utility Function:** The utility of a buyer is their valuation minus their bid, multiplied by the probability of winning.
    * $U_1(\theta_1, \theta_2, b_1, b_2) = (\theta_1 - b_1) \times P(b_1 > b_2)$
* **Risk Neutrality Assumption:** Because buyers are risk-neutral, their bidding strategy is a linear function of their valuation: $b_i = \alpha_i \theta_i$.
* **Uniform Distribution Assumption:** Because valuations are uniformly distributed, the probability of buyer 1 winning (i.e., $b_1 > b_2$) is a linear function of their bid.
* **Maximizing Utility:** Each player must choose a bidding strategy ($b_1, b_2$) to maximize their utility. This leads to a set of equations where the optimal bid for each player is found to be a function of the other player's bidding strategy.
* **Bayesian Nash Equilibrium:** A BNE is a set of strategies where each player's strategy is a best response to the strategies of the other players. By solving the system of equations, it is shown that the only stable solution is for both players to bid half of their valuation.
    * The strategies $b_1 = \frac{1}{2}\theta_1$ and $b_2 = \frac{1}{2}\theta_2$ form a BNE.

---

### 5. Generalization to N Players

The lecture extends the theorem to a more general case with $N$ players.

* **Theorem (N Players):** The strategy of bidding $\frac{N-1}{N}$ times your valuation, i.e., $b_i = \frac{N-1}{N}\theta_i$, for each buyer $i$ forms a Bayesian Nash Equilibrium.
* **Assumptions:**
    1.  There are $N$ buyers.
    2.  Buyers are risk-neutral.
    3.  Valuations are uniformly distributed in [0, 1].

---

### Keywords and Definitions

* **First-Price Auction:** "The player, the buyer, a buyer who bids the maximum wins the auction, and the winner obtains the object from the seller by paying his or her bid."
* **Bayesian Nash Equilibrium:** An equilibrium concept for games with incomplete information, where a player's strategy is a best response to the other players' strategies, given their beliefs about the others' private information.
* **Risk-Neutrality:** A player is indifferent between a certain outcome and a risky outcome with the same expected value.
* **Risk-Seeking:** A player prefers a risky outcome over a certain outcome with the same expected value.
* **Risk-Averse:** A player prefers a certain outcome over a risky outcome with the same expected value.
* **Uniformly Random Distribution:** A probability distribution where every value in a given range (e.g., 0 to 1) has an equal chance of being chosen.

---
Let's use a couple of examples to make the first-price auction concepts clearer.

### Example 1: Bidding Half Your Valuation

Imagine there are two buyers, Alice and Bob, bidding on a single item. Both are risk-neutral, and their valuations are uniformly distributed between 0 and 1. The main theorem states that the optimal strategy is to bid half of your valuation.

* **Alice's Valuation:** $\theta_{Alice} = \$0.80$
* **Bob's Valuation:** $\theta_{Bob} = \$0.60$

According to the theorem, they should bid half of their valuations:
* **Alice's Bid:** $b_{Alice} = 0.5 \times \$0.80 = \$0.40$
* **Bob's Bid:** $b_{Bob} = 0.5 \times \$0.60 = \$0.30$

**Result:** Alice's bid of $0.40 is higher than Bob's bid of $0.30. Alice wins the item and pays her bid of $0.40.

* **Alice's Utility:** Her valuation is $0.80, and she paid $0.40. Her utility is $\$0.80 - \$0.40 = \$0.40$.
* **Bob's Utility:** He lost and paid nothing. His utility is $0.

In this scenario, bidding half your valuation is the **Bayesian Nash Equilibrium**. Alice's optimal strategy is to bid $0.40, given her belief about Bob's uniform valuation and his rational strategy (bidding half his valuation). Bob's optimal strategy is to bid $0.30, for the same reasons.

***

### Example 2: Bidding with More Than Two Players

The theorem generalizes to $N$ players. The optimal strategy for a player is to bid $\frac{N-1}{N}$ times their valuation.

Imagine there are four buyers ($N=4$) in an auction.
* **Your Valuation:** $\theta_{You} = \$100$
* **Your Optimal Bid:** $b_{You} = \frac{4-1}{4} \times \$100 = \frac{3}{4} \times \$100 = \$75$.

By bidding $75, you are maximizing your expected utility, given your assumptions about the other three players' valuations and their strategies. This is the rational choice in this specific type of auction.