### Mechanism Design Without Money

This lecture introduces the concept of **mechanism design without money**, a field that addresses the challenge of creating desirable outcomes in strategic interactions when monetary transfers are not an option. It circumvents the assumptions of quasi-linear environments and provides an alternative way to bypass the impossibility results of the **Gibbard-Satterthwaite theorem**.

The main idea is to restrict the set of preferences that players (or voters) can have, rather than relying on money for incentives. The lecture focuses on a specific example: **voting with single-peaked preferences**.

---

### Single-Peaked Preferences

**Single-peaked preferences** are a specific type of preference profile that is assumed in many social choice problems, particularly in political or ideological contexts.

#### The Concept
- We assume that all alternatives (candidates) are ordered along a single **societal axis**. For example, from "most conservative" to "most liberal" or from "least costly" to "most costly."
- Each voter is assumed to have an ideal point or position on this axis.
- A voter's preferences are "single-peaked" if their liking for an alternative **decreases as the alternative gets further away from their ideal point** on the societal axis.
- **Example:** A voter whose ideal candidate is A3 will prefer A2 and A4 over A1 and A5, because A2 and A4 are closer to A3 on the axis. Their preference "peaks" at A3 and drops off as you move away.

#### Formal Definition
A preference profile is **single-peaked** if there exists a single societal order of alternatives (e.g., $A_1, A_2, ..., A_m$) with respect to which every voter's preference is single-peaked.

---

### The Median Voting Rule

The **median voting rule** is a specific social choice function (or voting rule) designed for a single-peaked domain.

#### How It Works
1.  All voters report their **most preferred alternative** (their "peak" preference).
2.  Based on the societal order, the votes are tallied.
3.  The winner is the candidate who is the **median of all the reported peaks**.
4.  If the number of voters is even, we can choose a tie-breaking rule, such as selecting the leftmost median candidate.

#### Key Properties of the Median Voting Rule

1.  **Dominant Strategy Incentive Compatible (DSIC):** This is a major result. The median voting rule is a rare example of a voting rule that is **strategy-proof**. This means that regardless of what any other voter does, it is always in a voter's best interest to truthfully report their most preferred candidate. The proof of this is based on the single-peaked nature of the preferences, which prevents a voter from manipulating the outcome to their benefit by lying.

2.  **Condorcet Winner:** The median voting rule always selects a **Condorcet winner**. A Condorcet winner is a candidate who is preferred by a majority (more than 50%) of the voters over any other single alternative.
    - The lecture mentions a slightly weaker version, a **weakly Condorcet winner**, who is preferred by **at least 50%** of voters over any other candidate.
    - The existence of a Condorcet winner is not guaranteed in all voting scenarios, but it is guaranteed in a single-peaked domain.

---

### Summary

- **Mechanism design without money** uses restrictions on preferences to achieve desirable outcomes, bypassing the need for monetary incentives.
- The **single-peaked domain** is a natural and common setting where preferences follow a clear societal order.
- The **median voting rule** is a powerful example of a mechanism in this domain. It is **strategy-proof** (DSIC) and always selects a **Condorcet winner**, demonstrating that it is possible to design a truthful and fair mechanism even without using money.