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


Absolutely! Let’s unpack your professor’s utility function:  
> **\( u_i = a_i \cdot \theta_i - p_i \)**

This is a **standard utility function** used in auction theory and mechanism design. It looks simple, but every symbol carries deep meaning. Let’s break it down piece by piece — *exactly* what your professor meant.

---

### 🔍 Breakdown of the Utility Function:  
$$
u_i = a_i \cdot \theta_i - p_i
$$

#### ✅ \( u_i \): **Utility of bidder \( i \)**
- This is what the bidder **wants to maximize**.
- It represents their **net benefit** from participating in the auction.
- Higher \( u_i \) = happier bidder.

---

#### ✅ \( \theta_i \): **Private valuation (or type) of bidder \( i \)**
- This is the **true value** bidder \( i \) places on winning the item.
- Example: If you’re bidding on a painting, and you’d pay up to \$500 because you love it — then \( \theta_i = 500 \).
- This is **private information**: Only *you* know it. The seller and other bidders don’t know it for sure.
- In game theory, we call \( \theta_i \) the bidder’s **type**.

> 💡 Assumption: \( \theta_i \) is drawn from some known probability distribution (e.g., uniform on [0,1]), which all bidders know.

---

#### ✅ \( a_i \): **Allocation indicator (binary outcome)**
- This tells you **whether bidder \( i \) wins** the item or not.
- Usually:
  - \( a_i = 1 \) → bidder \( i \) **wins**
  - \( a_i = 0 \) → bidder \( i \) **loses**

So $a_i \cdot \theta_i$ means:
- If you win (\( a_i = 1 \)), you get value \( \theta_i \)
- If you lose (\( a_i = 0 \)), you get value 0

> 📌 So \( a_i \cdot \theta_i \) = **the value you receive from winning** (if you win).

---

#### ✅ \( p_i \): **Payment made by bidder \( i \)**
- This is how much money bidder \( i \) has to **pay** to the seller.
- In a first-price auction: \( p_i = \) your own bid
- In a second-price (Vickrey) auction: \( p_i = \) the second-highest bid
- Could be zero if you lose

> ⚠️ Important: Payment only happens if you win — but even if you lose, sometimes \( p_i = 0 \), so it's fine.

---

### ✅ Putting It All Together:  
$$
u_i = a_i \cdot \theta_i - p_i
$$

> **“My utility = (Value I get from winning) minus (What I pay)”**

#### 🧠 Examples:

| Scenario                                                  | \( \theta_i \) | \( a_i \) | \( p_i \) | \( u_i \)                              |
| --------------------------------------------------------- | -------------- | --------- | --------- | -------------------------------------- |
| You win a painting worth \$500, and you bid \$300 and win | 500            | 1         | 300       | 500 – 300 = **200**                    |
| You win same painting, but pay \$600 (overbid!)           | 500            | 1         | 600       | 500 – 600 = **–100** (you lose money!) |
| You lose the auction                                      | 500            | 0         | 0         | 0 – 0 = **0**                          |

> ✅ Even if you value the item highly, if you pay more than your value, you’re worse off than not winning!

---

### 🤔 Why Is This Form So Important?

This structure is the **foundation of incentive compatibility** in auctions.

- Bidders want to **maximize** \( u_i \)
- The auction designer chooses rules (how to set \( a_i \) and \( p_i \)) based on bids
- But bidders might lie about their true \( \theta_i \) to get a better deal!

➡️ So the key question becomes:  
> **Can we design an auction where the best strategy for every bidder is to truthfully report $\theta_i$?**

That’s called **truthful bidding**, and it’s the goal of mechanisms like the **Vickrey auction**.

In a Vickrey auction:
- You bid your true value $b_i = \theta_i$
- You win if your bid is highest → $a_i = 1$
- You pay the second-highest bid → $p_i = \max_{j \ne i} b_j$

Then your utility is:
$$
u_i = 
\begin{cases}
\theta_i - \max_{j \ne i} \theta_j & \text{if you win} \\
0 & \text{if you lose}
\end{cases}
$$

And guess what? **Truth-telling is a dominant strategy** — no matter what others do, you can’t do better by lying!

---

### 🎯 Connection to Bayesian Games (from earlier!)

Remember: In Bayesian games, players have types (\( \theta_i \)) and choose actions (bids) based on those types.

The utility function \( u_i = a_i(\mathbf{b}) \cdot \theta_i - p_i(\mathbf{b}) \) defines the **payoff** that depends on:
- The **bid vector** \( \mathbf{b} = (b_1, b_2, ..., b_n) \)
- Which determines who wins (\( a_i \)) and how much they pay (\( p_i \))

A **Bayesian Nash Equilibrium** is a set of bidding strategies \( b_i(\theta_i) \) such that each bidder maximizes their **expected utility**, given their belief about others’ types.

So this utility function is the engine driving the whole strategic analysis.

---

### ✅ Final Summary (Simple Version)

Your professor’s formula:  
> **\( u_i = a_i \cdot \theta_i - p_i \)**

Means:
> “I get **value** from winning the item (**θᵢ**) only if I actually win (**aᵢ=1**), and I subtract what I have to **pay** (**pᵢ**).”

- If you win and pay less than your value → you’re happy!
- If you win and pay more than your value → you lost money!
- If you lose → you pay nothing and get nothing → utility = 0

This simple equation is the **core of auction theory** — everything else (equilibria, revenue, efficiency, truthful mechanisms) builds on this.

---

### 💡 Pro Tip for Exams/Problem Sets

When asked:  
> “What is the bidder’s utility?”  
Just write:  
> “The bidder’s utility is \( u_i = a_i \theta_i - p_i \), where \( \theta_i \) is their private value, \( a_i = 1 \) if they win, and \( p_i \) is their payment.”

You’ll sound like a pro 😎

Let me know if you want to see how this leads to optimal bidding strategies in first-price vs second-price auctions — I’ll walk you through the math!