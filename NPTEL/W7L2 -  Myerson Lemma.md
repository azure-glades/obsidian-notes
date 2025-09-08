### Single-Parameter Domains and Myerson's Lemma

This lecture introduces the concept of a **single-parameter domain**, a special class of settings in mechanism design, and a key result within this domain known as **Myerson's Lemma**.

#### What is a Single-Parameter Domain?

A **single-parameter domain** is a simplified setting where each player's private information, or "type" ($\theta_i$), can be represented by a single real number, typically their valuation.

- **Formal Definition:**
    - The type set for each player, $\Theta_i$, is a real number interval.
    - Player *i*'s valuation, $v_i$, for a specific allocation, *k*, can be simplified. It is equal to their type $\theta_i$ if they "win" (i.e., the allocation belongs to a specific winning set $K_i$), and it is 0 otherwise.
    - $v_i(k, \theta_i) = \theta_i$ if $k \in K_i$
    - $v_i(k, \theta_i) = 0$ if $k \notin K_i$
    - This structure is common in auctions where a bidder's type is their valuation for a single item.

#### Monotone Allocation Rules

A key concept in single-parameter domains is a **monotone allocation rule**.

- **Definition:** An allocation rule is monotone if, for a fixed type profile of all other players ($\theta_{-i}$), a player who wins with a certain type ($\theta_i$) will continue to win if their type increases to $\theta_i'$.
    - If a player wins at $\theta_i$, they will also win at any $\theta_i' \ge \theta_i$.
    - **Crucially**, this property relies on the fact that types are ordered along a real line.

- **Relationship with Allocative Efficiency:**
    - Every **allocatively efficient** allocation rule is **monotone**. This is intuitive: if an allocation maximizes the sum of valuations, a player with a higher valuation is more likely to be part of that efficient outcome.
    - However, the reverse is not always true. There exist monotone allocation rules that are **not** allocatively efficient. This means the set of monotone rules is a strict superset of the allocatively efficient rules in this domain.

---

### Myerson's Lemma

Myerson's Lemma is a powerful result that characterizes what can be implemented in a single-parameter domain. It extends the ideas of the VCG mechanism and provides a specific payment formula.

**Key Findings of the Lemma:**

1.  **Implementability:** An allocation rule $k^*$ is **implementable** (i.e., can be made dominant strategy incentive compatible) if and only if it is **monotone**.
    - This is a very strong characterization: it says that monotonicity is both a necessary and a sufficient condition for implementability in this context.

2.  **Unique Payment Scheme:** For any monotone allocation rule, there exists a unique payment scheme that makes it DSIC, provided that "zero-bidding" players pay zero.
    - This means if you have a monotone allocation rule, you don't need to guess about the payment scheme; there is only one "right" way to set payments to make it work.

3.  **Payment Formula:** The lemma provides an explicit formula for this unique payment rule. For a winning player *i* with type $\theta_i$, the payment is given by:
    - $T_i(\theta_i, \theta_{-i}) = - \int_0^{\theta_i} \frac{\partial k_i(z, \theta_{-i})}{\partial z} dz$
    - The negative sign indicates a payment is made. This formula shows that the payment is an integral over the change in the player's allocation probability or status as their type increases.
    - **In simpler terms:** The payment is based on a player's **critical value**—the lowest bid at which they would win, given the bids of everyone else. The payment is the negative of the critical value, which means they pay an amount equal to their critical value.

- **Connection to VCG:** The payment rule in Myerson's Lemma is very similar to the VCG payment, which is based on the concept of an externality. Myerson's formula generalizes this idea for the single-parameter domain.

> In simple terms, Myerson's Lemma gives us a complete recipe for designing truthful mechanisms in this important class of problems. It provides both the condition for success (monotonicity) and the exact payment formula to achieve it.

---

### Summary and Next Steps

- **Single-parameter domains** simplify mechanism design problems where a player's private information can be captured by a single number.
- **Monotone allocation rules** are a key concept in this domain, defined by the property that increasing a player's type cannot make them lose.
- **Myerson's Lemma** provides a powerful result: any monotone allocation rule is implementable, and the lemma gives the explicit payment formula to achieve this.
- The next lecture will explore a concrete application of Myerson's Lemma in an important use case.