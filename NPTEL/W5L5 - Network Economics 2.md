### Network Economics: Stability vs. Efficiency and the Co-Authorship Model

This lecture continues the discussion on strategic network formation by examining **pairwise stability** in detail and comparing it to **efficiency**, highlighting the frequent conflict between these two concepts. It then introduces a new model, the **co-authorship network model**, to further illustrate this conflict.

---

### 1. Recap: Efficient Networks with Distance-Based Utility

The lecture begins by recapping the findings from the previous session regarding efficient networks with a distance-based utility function.

* **Utility:** A player's utility is the sum of benefits from all connections minus the total cost of forming direct links.
    $U_i(G) = \sum_{j \neq i} B(L_{ij}) - C \cdot d_i$
* **Efficient Networks:** The structure of the most efficient network depends on the cost of forming a link ($C$) relative to the benefits of direct ($B_1$) and indirect ($B_2$) connections.
    1.  If $C < B_1 - B_2$: The **Complete Network** is most efficient.
    2.  If $B_1 - B_2 \le C \le B_1 + (n-2)B_2$: The **Star Network** is most efficient.
    3.  If $C > B_1 + (n-2)B_2$: The **Empty Network** is most efficient.

---

### 2. Pairwise Stable Networks with Distance-Based Utility

Now, the lecture introduces the proof for which networks are **pairwise stable** under the same distance-based utility model.

* **Pairwise Stable Network Definition:** A network where:
    * No two players with an existing link want to delete it.
    * No two players without a link want to form one.
* **Pairwise Stable Networks based on Cost (C):**
    1.  If $C < B_1 - B_2$: The **Complete Network** is the **unique pairwise stable network**.
        * **Proof:** If $C < B_1 - B_2$, it implies $B_1 - C > B_2$. The benefit of a direct link ($B_1 - C$) is always greater than the benefit of the best indirect link ($B_2$). Therefore, any two players not directly connected would have a mutual incentive to form a link. This dynamic leads to a complete network where no further links can be formed.
    2.  If $B_1 - B_2 \le C < B_1$: A **Star Network** is pairwise stable, but it is **not necessarily unique**.
        * **Proof:**
            * **No deletion:** The central node will not delete a link because $B_1-C > 0$, so a positive benefit would be lost. A peripheral node will not delete its link to the center as its payoff would drop to zero.
            * **No new links:** Two peripheral nodes will not form a direct link because the benefit ($B_1-C$) is less than the benefit of their indirect connection ($B_2$).
    3.  If $C > B_1$: A pairwise stable network will either be the **Empty Network** or a network where every node has a degree of at least 2.

### 3. The Conflict Between Stability and Efficiency

By comparing the results for efficient and pairwise stable networks, the lecture illustrates their conflict.

* **Coincidence:** When $C < B_1 - B_2$, the **complete network** is both the unique efficient and the unique pairwise stable network.
* **Conflict:** In the range $B_1 - B_2 \le C < B_1$, the **star network** is the most efficient, but it is not the only pairwise stable network. In fact, a network can be efficient (like the star) but unstable if players have an incentive to rearrange links. This is a common theme in network economics.

---

### 4. Co-Authorship Network Model

The lecture introduces a new model to demonstrate the stability-efficiency conflict with a different utility function.

* **Utility Function:** A player's utility is derived from their connections, but the benefit is inversely related to the degree of their connections.
    * $U_i(G) = \sum_{j \text{ is a neighbor of } i} \left( \frac{1}{d_i d_j} \right) + \sum_{j \text{ is a neighbor of } i} \left( \frac{1}{d_j} \right) + 1$
    * $d_i$ is the degree (number of connections) of player $i$.
* **Intuition:** The utility of a collaboration is higher if your partner is not collaborating with many other people. You get more of their attention.

#### Efficient Network in the Co-Authorship Model

* **Total Utility:** The goal is to maximize $\sum U_i(G)$.
* **Proof:** By simplifying the total utility function, it is shown that the total utility is maximized when the degrees of all players are minimized.
* **Result:** The most efficient network consists of a set of **disjoint pairs**. This maximizes the total utility because it gives every player a degree of 1, which maximizes the individual benefit from each collaboration.

#### Pairwise Stable Network in the Co-Authorship Model

* **Analysis:** The lecture analyzes the conditions under which a player $i$ has an incentive to form a new link with player $j$.
* **Condition for forming a link:** A link will be formed if the benefit from the new link is greater than the cost. It is shown that if player $i$'s degree ($d_i$) is similar to player $j$'s degree ($d_j$), they will have a strong incentive to form a link. The specific condition is derived to be related to the degrees of the players.
* **Result:** Pairwise stable networks in this model are those where players with similar degrees are connected.

#### Conflict in the Co-Authorship Model

* **Efficient vs. Stable:** The efficient network in this model is a set of disjoint pairs (everyone has a degree of 1). However, this network is **not pairwise stable**.
* **Unstable Pairs:** A player in one pair has an incentive to form a link with a player in another pair because their degrees are equal. This would lead to a more connected network, but it would decrease the total utility.
* **Conclusion:** The efficient network (disjoint pairs) is pairwise unstable because players have a selfish incentive to form new links that ultimately lower the total welfare of the system. This perfectly illustrates the central conflict between stability and efficiency.