### Auction Theory: First-Price vs. Second-Price Auctions

This lecture continues the study of auctions, contrasting the **First-Price Auction** with the **Second-Price Auction (Vickrey Auction)**. The main focus is on the concept of **dominant strategy incentive compatibility (DSIC)** and proving that the second-price auction possesses this desirable property.

---

### 1. The First-Price Auction and Its Flaw

A **first-price auction** is a type of auction where all bidders simultaneously submit sealed bids. The highest bidder wins the item and pays the exact price they submitted.

Here are its key characteristics:
- **Simultaneous Sealed Bids:** All bidders submit their bids at the same time, without knowing what anyone else has bid. This is often called a "blind auction."
- **Winner:** The bidder who submits the highest bid wins the item.
- **Payment:** The winner pays the full amount of their winning bid.

This type of auction is used in many different contexts, from government contracts to online advertising. A key aspect of a first-price auction is that it's not a "truthful" mechanism. This means that a bidder's optimal strategy is often to bid less than their true valuation of the item to avoid overpaying, which requires them to think strategically about what their competitors might be bidding.

* **The Problem:** The first-price auction is **not DSIC**. This means bidding your true valuation is not always the best strategy.
* **Example:** In a scenario with two sellers and a buyer, a seller with a true valuation of 10 can increase their utility by bidding 14 instead of their true valuation. By bidding 14, they still win the auction but receive a higher payment, thus misreporting their true valuation for a better payoff. This makes the auction strategically complex and non-truthful.


> [!NOTE] DISC - Dominant Strategy Incentive Compatible
>  **Dominant Strategy Incentive Compatible (DSIC)** is a fundamental concept in game theory. A mechanism (like an auction or a voting system) is DSIC if truth-telling is the best strategy for every participant, **regardless of what any other participants do**.
>  - **"Dominant Strategy"**: Your optimal choice is clear and doesn't depend on guessing what others will do. The strategy of being honest **dominates** all other possible strategies.
>  - **"Incentive Compatible"**: The system is designed so that the incentives of the bidder is aligned with that of the auctioner.


---

### 2. The Second-Price Auction (Vickrey Auction)

The second-price auction is a proposed solution to the flaws of the first-price auction.

* **Allocation Rule:** This is the same as the first-price auction. The seller with the lowest bid wins the auction.
* **Payment Rule:** This is where the difference lies. The winning seller receives a payment equal to the **second-lowest bid** among all other sellers. This is why it's called a second-price auction.
* **Key Theorem:** "Bidding valuations is a weakly dominant strategy equilibrium for the second price auction." This means that for every player, bidding their true valuation is the best strategy, regardless of what the other players bid.

---

### 3. Proof of Dominant Strategy Incentive Compatibility (DSIC)

The lecture provides a detailed proof to show that truthful bidding is a weakly dominant strategy in a second-price auction. The proof considers two cases for any given player, Player $i$, whose true valuation is $\theta_i$.

* **Case 1: Player $i$ wins by bidding truthfully ($s_i^* = \theta_i$).**
    * This means $\theta_i \le \lambda_i$, where $\lambda_i$ is the lowest bid from all other players.
    * **Player $i$'s utility:** $U_i = \lambda_i - \theta_i$. Since $\theta_i \le \lambda_i$, the utility is non-negative ($U_i \ge 0$).
    * **What if Player $i$ deviates to bid $s_i \neq \theta_i$?**
        * If Player $i$ still wins, their payment is still $\lambda_i$, so their utility remains the same.
        * If Player $i$ now loses, their utility becomes 0.
        * Conclusion: Any deviation from truthful bidding will not increase Player $i$'s utility in this case.

* **Case 2: Player $i$ loses by bidding truthfully ($s_i^* = \theta_i$).**
    * This means $\theta_i > \lambda_i$.
    * **Player $i$'s utility:** $U_i = 0$.
    * **What if Player $i$ deviates to bid $s_i < \theta_i$?**
        * If Player $i$ still loses, their utility remains 0.
        * If Player $i$ now wins, they will sell the item for a price of $\lambda_i$. Their utility becomes $U_i = \lambda_i - \theta_i$. Since $\theta_i > \lambda_i$, this utility is negative ($U_i < 0$).
        * Conclusion: A deviation that causes Player $i$ to win when they would have lost truthfully results in a negative utility, which is worse than the original utility of 0.

* **Final Conclusion:** In all scenarios, a player's utility does not increase by deviating from their true valuation. This proves that truthful bidding is a **weakly dominant strategy**. The lecturer notes that this is also a unique weakly dominant strategy.

---

A **second-price auction** is a type of sealed-bid auction where the highest bidder wins the item but pays a price equal to the second-highest bid.
Here's a breakdown of how it works and why it's used:
- **Sealed Bids:** All bidders submit their bids simultaneously and in secret, without knowing what others have offered.
- **Winner:** The bidder who submits the highest bid is the winner.
- **Payment:** The winner doesn't pay their own bid. Instead, they pay the amount of the second-highest bid.
This type of auction, also known as a **Vickrey auction**, has a significant game-theoretic advantage over a first-price auction: it is **dominant strategy incentive compatible (DSIC)**. This means the optimal strategy for every player is to bid their true valuation for the item. They are incentivized to be truthful because they know that even if they bid very high and win, they will only pay the price of the second-highest bid, which prevents them from overpaying.

### 4. Why Second-Price Auctions Are Desirable

* **For Bidders:** The job of a bidder is simplified. They don't need to perform complex strategic analysis; they can simply bid their true valuation and know that it is the best possible strategy.
* **For Auctioneers:** The auctioneer learns the true valuations of all the sellers, which can be useful for other purposes.
* **Allocative Efficiency:** This type of auction is also **allocatively efficient**, meaning the item is sold by the bidder who values it the least (i.e., the lowest bid wins), which is the most efficient outcome for the market.

---

### Keywords and Definitions

* **Dominant Strategy Incentive Compatible (DSIC):** "A property of an auction where telling the truth (bidding your true valuation) is a dominant strategy for each player."
* **Allocatively Efficient:** "A property of an auction where the item is sold by the bidder who values it the least."
* **Weakly Dominant Strategy:** A strategy that is at least as good as any other strategy, regardless of what the other players do, and is strictly better in some cases.
* **Second-Price Auction:** "The winning seller receives the lowest of all other sellers' bids."