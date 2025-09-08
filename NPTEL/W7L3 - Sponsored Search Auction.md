### Sponsored Search Auctions

This lecture provides a concrete application of **Myerson's Lemma** to a common online scenario: **sponsored search auctions**.

#### The Setting

- **Objective:** Search engines (e.g., Google, Amazon) need to decide which advertisers' sponsored links to display alongside search results and in which order. The goal is to maximize the platform's revenue while also providing a good user experience.
- **Participants:**
    - **Advertisers:** These are the bidders. Each advertiser *i* has a private **valuation**, $v_i$, which represents the value they get if a user clicks on their ad.
    - **Search Engine:** The auctioneer, who sells the ad space.
- **Resources:** There are *k* ad slots available on the search page. The value of these slots varies, with the top slot being the most valuable.
- **Click-Through Rate (CTR):** The difference in slot value is measured by **click-through rates (CTRs)**, denoted by $\alpha_1, \alpha_2, ..., \alpha_k$. We assume the slots are ordered by their CTR, with $\alpha_1 \ge \alpha_2 \ge ... \ge \alpha_k$.
- **Ad Quality:** Each advertiser's ad has a **quality score**, $\beta_i$, between 0 and 1.
- **Probability of a Click:** The probability that a user clicks on advertiser *i*'s ad when it's shown in slot *j* is given by the product of the ad's quality and the slot's CTR: $\beta_i \times \alpha_j$.

#### The Single-Parameter Domain

This sponsored search auction setting fits into the framework of a **single-parameter domain** because each advertiser's "type" can be represented by a single real number, their valuation, $v_i$.

- The advertiser's utility from a given allocation (being shown in a specific slot) is the product of their valuation and the probability of a click. For example, if advertiser *i*'s ad is shown in slot *j*, their value is $v_i \times (\beta_i \times \alpha_j)$. This is also known as the **bid value**, $b_i = v_i \beta_i$.

- **Efficient Allocation:** To maximize the sum of valuations, an **allocatively efficient rule** would allocate the slots to the advertisers who have the highest "bid values" ($v_i \beta_i$). The top *k* advertisers with the highest bid values would get a slot, and they would be ordered according to the slots' CTRs. The advertiser with the highest bid value gets the slot with the highest CTR, the second-highest bidder gets the second-highest CTR slot, and so on.

#### Applying Myerson's Lemma to Payments

Because this is a single-parameter domain, we can apply **Myerson's Lemma** to determine the unique payment scheme that is **DSIC (dominant strategy incentive compatible)**.

- **The Payment Formula:** The payment for a winning advertiser is based on the **critical value** at which they "win" a slot. The payment is derived by integrating the allocation function.
- In this specific case, the payment formula results in a payment for advertiser *i* that is based on the valuations of the players ranked below them in the auction.

- **Example Payment Calculation (Simplified):** Let's consider the advertiser with the highest bid value, $v_1 \beta_1$. This advertiser will get the top slot with a CTR of $\alpha_1$.
    - The payment for this advertiser ($T_1$) is determined by the valuations of the other bidders. In a basic Vickrey-like auction, the payment would be the second-highest bid value.
    - However, due to the different CTRs of the slots, the payment is a bit more complex. The payment made by advertiser *i* who wins the $i$-th slot is:
        - $T_i = \frac{v_{i+1} \beta_{i+1}}{\alpha_{i}} \times \alpha_{i+1}$ (This isn't the final result from the lecture, but it represents the underlying idea of paying based on the valuation of the next-ranked bidder and the difference in slot values).

- **Corrected Formula based on lecture notes:**
    - The final payment made by player *i* (who wins a slot) is determined by the valuations of the players ranked below them. The calculation involves a sum over the rectangles in the area plot of the allocation function.
    - The payment for the player who wins the $i$-th slot is essentially the product of the next-ranked bidder's bid value and the ratio of the CTRs of the two slots.

#### Key Takeaway

- The sponsored search auction is a perfect example of a **single-parameter domain** in practice.
- **Myerson's Lemma** provides the theoretical foundation for designing a payment rule that ensures advertisers have a strong incentive to bid their **true valuations**.
- The unique payment scheme, derived from the lemma, ensures that the auction is **dominant strategy incentive compatible**, which makes it a very efficient and robust mechanism for allocating ad space.
- The payment is structured so that a winning advertiser pays based on the **critical value** of the next-highest ranked bidder, adjusted for the different values of the ad slots.