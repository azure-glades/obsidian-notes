### Network Economics: Strategic Network Formation
[[W5L4.1 --- In Simpler Words]]  [[W5L4.2 --- Efficient Network Structure]]
This lecture introduces the fundamental concepts of **network economics**, focusing on strategic network formation where agents choose to form links based on self-interest. It defines key concepts like stability and efficiency and analyzes a specific model with distance-based utility functions.

---

### 1. Introduction to Strategic Networks

* **Random vs. Strategic Networks:**
    * **Random Network Formation:** Links are formed randomly or probabilistically (e.g., the spread of a virus like COVID).
    * **Strategic Network Formation:** Players choose to form or sever links based on mutual benefit. This is the primary focus of the lecture.
* **Two Core Issues in Strategic Networks:**
    1.  **Stability:** Addresses the individual incentives of players to form or delete links.
    2.  **Efficiency:** Concerned with maximizing the total welfare (total utility) of all players in the network.
    * The lecture highlights that stability and efficiency are often in conflict.

> [!NOTE] Stability
> **Stability** focuses on **individual incentives**. A network is considered stable if no player or small group of players has a reason to change it. The lecture specifically defines **pairwise stability** as a key form of stability:
> - **No one wants to break a link:** If two players are connected, neither player has an incentive to sever that connection.
> - **No one wants to form a new link:** If two players are _not_ connected, they do not have a mutual incentive to form a link. In other words, adding the link wouldn't make both of them better off.    

This concept is rooted in the idea of individual rationality, similar to a Nash Equilibrium in game theory. A stable network represents a situation where individual self-interest prevents any single player or pair from deviating from the current network structure. However, a stable network may not always exist.

> [!NOTE] Efficiency -> Social Utility
> **Efficiency**, on the other hand, focuses on **social welfare**. A network is considered efficient if it maximizes the **total utility** (or sum of payoffs) of all the players in the network.
> - The goal of efficiency is to find the network that provides the greatest collective good for all members, regardless of how that total utility is distributed among them.
> - An efficient network is also considered **Pareto-efficient**, meaning you can't find another network that makes at least one player better off without making anyone else worse off.

The conflict arises because a network that is stable due to individual self-interest may not be the one that produces the greatest total welfare. A network with high total utility might be unstable if some players could get an even higher individual payoff by changing a link. The lecture's example of the efficient red network being unstable illustrates this perfectly.

### 2. Notations and Utility

* **Players:** A set of $n$ players, labeled $1, 2, \dots, n$.
* **Network (G):** A specific graph representing connections between players. $G_n$ is the set of all possible networks among $n$ players.
* **Utility ($U_i(G)$):** The payoff for player $i$ in network $G$. This represents the total benefits minus the total costs from all connections.

---

### 3. Stability in Networks: Pairwise Stability

* **Definition:** A network $G$ is called **pairwise stable** if it satisfies two conditions:
    1.  **No incentive to delete a link:** For every existing edge $(i, j)$ in $G$, both players $i$ and $j$ must have a payoff in $G$ that is greater than or equal to their payoff in the network $G - (i,j)$ (the network with the link removed). No player wants to sever an existing tie.
    2.  **No incentive to add a link:** For every non-existing edge $(i, j)$ in $G$, it is not the case that both players $i$ and $j$ would be strictly better off by adding the link. No two unconnected players have a mutual incentive to form a new tie.
* **Limitations of Pairwise Stability:**
    * It assumes that deviations are made by one or two players at a time, but in reality, a large-scale reorganization of links might be beneficial.
    * A pairwise stable network is not guaranteed to exist. The lecture gives an example of a 4-player network that cycles between different configurations without settling on a stable state.

---

### 4. Efficiency in Networks

* **Efficient Network:** A network that maximizes the sum of all players' utilities. An efficient network is one that maximizes the total social welfare.
    * **Definition:** A network $G$ is efficient if $\sum_{i=1}^{n} U_i(G) \ge \sum_{i=1}^{n} U_i(G')$ for all other networks $G'$ in the set of all possible networks.
* **Pareto-Efficient Network:** A network where no other network exists that could make at least one player better off without making any other player worse off.
* **Relationship:** **An efficient network is always Pareto-efficient.** The logic is that if a network is efficient, its total utility is at a maximum. To move to another network where a player is strictly better off, the total utility would have to increase, which contradicts the definition of an efficient network.
* **Conflict:** An efficient network is not necessarily pairwise stable, and a pairwise stable network is not necessarily efficient. The lecture gives an example of a network that is efficient but unstable because two players have an incentive to form a new link.

> [!NOTE] Pareto Efficiency
> **Pareto efficiency** is a situation where you can't reallocate resources or make any changes to a system to make one person better off without making someone else worse off. It's a state of "no-waste" or maximum economic efficiency.
> Ex:
> - **Trade:** This is the most common example. When two people voluntarily trade, both are better off (they get something they value more than what they gave up) and no one is worse off. A series of such trades, called a **Pareto improvement**, continues until no more mutually beneficial trades can be made. The final state is Pareto efficient.
> - **The Pie Analogy:** Imagine you have a pie and three people.
> 	- **Inefficient:** The pie is just sitting on the table. You could give it to one person without making anyone else worse off (they get no pie either way). This is a **Pareto improvement**.
> 	- **Efficient (but Unequal):** You give the entire pie to one person. This is now a Pareto-efficient allocation. Why? Because you can't give a slice of the pie to a second person without taking it away from the first person, making them worse off.


![[Pasted image 20250823185226.png]]

---
### 5. The Distance-Based Utility Model

This model provides a concrete framework to analyze efficiency and stability.

* **Utility Function:** A player's utility is based on the benefits from connections minus the cost of forming those connections.
    * $U_i(g) = \sum_{j \neq i} b(l_{ij}(g)) - C \cdot d_i(g)$
    * $L_{ij}$ is the minimum path distance between player $i$ and $j$.
    * $B(k)$ is the benefit derived from a connection at distance $k$. The benefit decreases as the distance increases, so $B(k) > B(k+1)$. distance (k) is the number of nodes on the path from i to j
    * $C$ is the cost of forming a link.
    * $d_i$ is the number of links player $i$ has (their degree).

#### Efficient Network Structures

Based on the relationship between the cost of a link ($C$) and the benefits of direct ($B_1$) and indirect ($B_2$) connections, the lecture proves that the efficient network structure is one of three types:

1.  **Complete Network:** A network where every player is connected to every other player.
    * **Condition:** $$C < b(1) - b(2)$$
    * **Logic:** Cost of forming a direct link is much lesser than connecting through an indirect, longer link. I.e every node prefers to form a connection of distance 1 (i.e direct link) over an indirect link thats longer distance
2.  **Star Network:** A network with one central player connected to all other players, who are only connected to the central player.
    * **Condition:** $$b(1) - b(2) \le C \le b(1) + \frac{(n-2)}{2}b(2)$$
    * **Logic:** The star network maximizes the total utility in this cost range. The central player's utility comes from many direct links, while peripheral players benefit from indirect connections through the center.
3.  **Empty Network:** A network with no links at all.
    * **Condition:** $$C > b(1) + \frac{(n-2)}{2}b(2)$$
    * **Logic:** The cost of forming a link is so high that it outweighs any potential benefits. The total utility of any connected network would be negative, so the empty network, with a total utility of zero, is the most efficient.

---

### 6. What's Next?

The next lecture will continue this discussion by analyzing the **pairwise stable networks** under the same distance-based utility model and will compare them to the efficient network structures. This will further explore the conflict between stability and efficiency and will also introduce a different model, the **co-authorship network model**.