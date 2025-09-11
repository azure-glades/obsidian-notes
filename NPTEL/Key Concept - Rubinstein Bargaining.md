Absolutely! The **Rubinstein Bargaining Game** (often spelled *Rubinstein*, after Ariel Rubinstein) is one of the most elegant and foundational models in game theory for studying **strategic bargaining** between two players over the division of a surplus (e.g., a pie of size 1). It’s a **sequential, alternating-offer bargaining game with infinite horizon and discounting**, and it yields a unique **Subgame Perfect Equilibrium (SPE)** — which is rare and beautiful in infinite games.

---

## 🎯 1. Basic Setup

### Players:
- Two players: Player 1 and Player 2.

### Resource:
- A divisible “pie” of size **1** to be split.

### Protocol:
- Players alternate making offers, starting with Player 1 in period 0.
- In each period t = 0, 1, 2, ..., the player whose turn it is proposes a split:  
  → e.g., “I take x, you take 1−x”.
- The other player can either **Accept** (game ends, payoffs realized) or **Reject** (game moves to next period, and the other player proposes).
- **If an offer is rejected, the game continues.**

### Discounting:
- Future payoffs are discounted by a factor δ₁ ∈ (0,1) for Player 1, and δ₂ ∈ (0,1) for Player 2.
- This captures **impatience**: a payoff of 1 tomorrow is worth only δ today.

> 💡 Interpretation: δ can represent time preference, probability the game ends, or cost of delay.

---

## 📈 2. Payoffs

If agreement is reached in period t on a split (x, 1−x), where x goes to the proposer:

- Proposer gets: **δ^t ⋅ x**
- Responder gets: **δ^t ⋅ (1−x)**

If no agreement is ever reached, both get **0**.

---

## 🔍 3. Goal: Find Subgame Perfect Equilibrium (SPE)

We want to find strategies for both players such that:

- At every point in the game (after any history), no player can gain by deviating.
- Uses **backward induction logic**, even though the game is infinite.

> 🎯 Key Insight: Because of discounting, delay is costly → players have incentive to reach agreement quickly.

---

## 🧮 4. Solving the Game — The Unique SPE

Let’s denote:

- **V₁** = equilibrium payoff to Player 1 (when it’s her turn to propose)
- **V₂** = equilibrium payoff to Player 2 (when it’s his turn to propose)

### Step 1: Suppose we’re in a subgame where Player 2 is about to propose.

Player 2 knows that if he offers Player 1 anything less than what she could get by waiting (and proposing next period), she’ll reject.

→ So Player 2 must offer Player 1 at least **δ₁ ⋅ V₁** (because if she rejects, she’ll get V₁ next period, discounted to today).

→ Therefore, Player 2 offers:  
  **x₁ = δ₁ ⋅ V₁** to Player 1,  
  and keeps **1 − x₁ = 1 − δ₁ ⋅ V₁** for himself.

So:  
> **V₂ = 1 − δ₁ ⋅ V₁**

---

### Step 2: Now suppose Player 1 is proposing.

She knows that if Player 2 rejects, he’ll get to propose next period and earn V₂, which is worth **δ₂ ⋅ V₂** to him today.

→ So Player 1 must offer Player 2 at least **δ₂ ⋅ V₂**.

→ She offers:  
  **x₂ = δ₂ ⋅ V₂** to Player 2,  
  and keeps **1 − x₂ = 1 − δ₂ ⋅ V₂** for herself.

So:  
> **V₁ = 1 − δ₂ ⋅ V₂**

---

### Step 3: Solve the System of Equations

We now have:

1. V₂ = 1 − δ₁ V₁  
2. V₁ = 1 − δ₂ V₂

Substitute (1) into (2):

> V₁ = 1 − δ₂ (1 − δ₁ V₁)  
> V₁ = 1 − δ₂ + δ₂ δ₁ V₁  
> V₁ − δ₁ δ₂ V₁ = 1 − δ₂  
> V₁ (1 − δ₁ δ₂) = 1 − δ₂  
>  
> ✅ **V₁ = (1 − δ₂) / (1 − δ₁ δ₂)**

Similarly, substitute back:

> V₂ = 1 − δ₁ ⋅ [(1 − δ₂)/(1 − δ₁ δ₂)]  
> = [ (1 − δ₁ δ₂) − δ₁(1 − δ₂) ] / (1 − δ₁ δ₂)  
> = [1 − δ₁ δ₂ − δ₁ + δ₁ δ₂] / (1 − δ₁ δ₂)  
> = (1 − δ₁) / (1 − δ₁ δ₂)

> ✅ **V₂ = (1 − δ₁) / (1 − δ₁ δ₂)**

---

## 🎁 5. Equilibrium Offers

### In period 0 (Player 1 proposes):

She offers Player 2 exactly his discounted continuation value:  
→ **Offer to Player 2: δ₂ ⋅ V₂ = δ₂ ⋅ (1 − δ₁)/(1 − δ₁ δ₂)**

So Player 1 keeps:  
→ **x₁* = 1 − δ₂ ⋅ V₂ = (1 − δ₂)/(1 − δ₁ δ₂) = V₁**

Player 2 accepts because he’s indifferent — getting δ₂ V₂ now = V₂ next period discounted.

> ✅ **Agreement reached immediately in period 0.**

---

## 📊 6. Intuition & Interpretation

- **More patient players (higher δ) get larger shares.**  
  If δ₁ > δ₂ → Player 1 is more patient → she can “wait out” Player 2 → gets bigger share.

- **First-mover advantage?** Yes — but it’s moderated by patience.  
  Even if δ₁ = δ₂ = δ, Player 1 gets (1−δ)/(1−δ²) = 1/(1+δ), Player 2 gets δ/(1+δ) → so Player 1 gets more.

  Example: δ = 0.9 → Player 1 gets 1/1.9 ≈ 52.6%, Player 2 gets 47.4%.

- **As δ → 1 (extremely patient)**, shares converge to 50-50 → no advantage to moving first.

- **As δ → 0 (extremely impatient)**, Player 1 takes almost everything → Player 2 must accept even tiny offers today rather than wait for nothing.

---

## 🔄 7. Why is this the Unique SPE?

- Rubinstein (1982) proved that under perfect information, alternating offers, discounting, and infinite horizon, **there exists a unique SPE** in pure stationary strategies.
- “Stationary” means: players make the same offer every time it’s their turn to propose, regardless of period — because the game structure is the same in every period (due to geometric discounting).

> 🧠 No delay in equilibrium — even though the game could go on forever, rational players agree immediately.

---

## 🆚 8. Comparison with Nash Bargaining Solution

The **Nash Bargaining Solution** (axiomatic) for two players with equal bargaining power gives 50-50 split.

Rubinstein’s model **endogenizes** the bargaining power via **patience** (δ₁, δ₂). The more patient you are, the more power you have.

In fact, as players become perfectly patient (δ₁, δ₂ → 1), the Rubinstein solution converges to Nash’s 50-50 — a beautiful consistency result.

---

## 📐 9. Mathematical Summary

| Concept                     | Formula                                      |
|----------------------------|----------------------------------------------|
| Player 1’s equilibrium payoff (proposer) | V₁ = (1 − δ₂) / (1 − δ₁ δ₂)                 |
| Player 2’s equilibrium payoff (if proposer) | V₂ = (1 − δ₁) / (1 − δ₁ δ₂)                 |
| Player 1’s opening offer to Player 2     | s₂ = δ₂ ⋅ V₂ = δ₂ (1 − δ₁)/(1 − δ₁ δ₂)      |
| Player 1’s share in period 0             | s₁ = 1 − s₂ = (1 − δ₂)/(1 − δ₁ δ₂) = V₁     |
| Agreement reached in                     | Period 0 (immediately)                      |

---

## 📚 10. Extensions & Variants

- **Finite horizon**: Game ends after T offers → solved by backward induction; last proposer takes all.
- **Different discount factors per period** → non-stationary equilibria.
- **Outside options** → players can quit and take an outside payoff.
- **Imperfect information** → e.g., private valuations → leads to delays and inefficiencies.
- **More than two players** → much more complex; no longer unique SPE.

---

## 💡 Why is Rubinstein Bargaining Important?

- It’s one of the few infinite-horizon games with a **unique, tractable SPE**.
- Shows how **patience = bargaining power**.
- Demonstrates that **alternating offers + discounting → immediate efficiency**.
- Foundation for modeling wage negotiations, international treaties, mergers, divorce settlements, etc.

---

## ✍️ Example Calculation

Let δ₁ = 0.8, δ₂ = 0.5

Then:

V₁ = (1 − 0.5) / (1 − 0.8×0.5) = 0.5 / (1 − 0.4) = 0.5 / 0.6 ≈ **0.833**

V₂ = (1 − 0.8) / 0.6 = 0.2 / 0.6 ≈ **0.333**

→ Player 1 offers Player 2: δ₂ V₂ = 0.5 × 0.333 ≈ **0.167**

→ Keeps **0.833** for herself → Player 2 accepts.

Player 1 gets 83.3% because she’s more patient (δ₁=0.8 > δ₂=0.5) AND moves first.

---

## 🧭 Conclusion

The **Rubinstein Bargaining Model** is a masterpiece of game theory — simple rules, elegant math, powerful intuition. It teaches us that in strategic bargaining:

> ⏳ **Time is power. Patience is leverage. And rational players don’t waste time.**

Let me know if you’d like to see the finite-horizon version, or how to introduce outside options or incomplete information! 🎯