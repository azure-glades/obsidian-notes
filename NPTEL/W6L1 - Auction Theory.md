### Introduction to Auction Theory and Bayesian Games

This lecture introduces game theory concepts applied to auctions. It defines the core elements of an auction from a game theory perspective and outlines the key questions and properties relevant to mechanism design.

---

#### 1. Types of Auctions

The lecture identifies two main types of auctions:
* **One buyer, multiple sellers:** An organization, like IIT Kharagpur, releases a tender, and multiple companies bid to sell a product or service. The lowest bid typically wins.
* **Multiple buyers, one seller:** The most common form of auction. Examples include:
    * The government auctioning public resources like spectrum or coal mines.
    * Sports leagues like the IPL auctioning players to different teams.

The core principles and analysis methods are similar for both types of auctions.

---

#### 2. Key Questions in Auction Theory

From a game theory perspective, two main questions are addressed:
1.  **Bidder's Strategy:** As a rational bidder, what should my bid be to maximize my utility? This assumes players are rational and intelligent and that the game's rules are common knowledge.
2.  **Auction Designer's Goal:** As the auctioneer, how can I design an auction that has desirable properties, such as being **dominant strategy incentive compatible (DSIC)** or **Bayesian incentive compatible (BIC)**?

---

#### 3. Auctions as Bayesian Games

An auction is framed as a **Bayesian game** because bidders have private information about their valuation of the item.

* **Players:** The set of players includes all buyers and sellers.
* **Outcomes:** An outcome is a tuple consisting of:
    * **Allocation:** Who gets (or gives) the item.
    * **Payment:** How much each player pays or receives.
* **Strongly Budget Balanced:** An auction is considered "strongly budget balanced" if the sum of all payments is zero, meaning no money is created or destroyed in the system.
* **Types ($\theta_i$):** The private information of each player, representing their valuation of the item.
* **Utility ($U_i$):** A player's utility is the value they get from the outcome. It depends on whether they receive the item and the payment they make.
    * **Formula:** $U_i = A_i \cdot \theta_i - P_i$
    * If a player receives the item ($A_i=1$), their utility is their valuation minus the payment ($\theta_i - P_i$).
    * If a player gives the item ($A_i=-1$), their utility is the payment they receive ($P_i$).
    * If a player does not get or give the item ($A_i=0$), their utility is their payment ($P_i$).
    * Note: The payment $P_i$ is positive if money is paid and negative if money is received.

---

### Keywords and Definitions

* **Strongly Budget Balanced:** "An auction where the sum of all payments is zero, so it neither generates nor receives any money from outside."
* **Dominant Strategy Incentive Compatible (DSIC):** "A property of an auction where telling the truth (bidding your true valuation) is a dominant strategy for each player." This means it's the best strategy regardless of what other players do.
* **Bayesian Incentive Compatibility (BIC):** "A property of an auction where telling the truth is the best strategy for each player given their beliefs about the other players' types." This is a weaker condition than DSIC.
* **Type ($\theta_i$):** "The set of all possible valuations of the item by player i. This is the private information of a player."