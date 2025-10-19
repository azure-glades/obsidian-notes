## Network Metrics for Importance 🕸️

### Betweenness Centrality
-   **Definition:** Measures how often a node acts as a **bridge** on the shortest path between other nodes.
-   **Formula:**
    $$
    \text{Betweenness}(k) = \sum_{i,j \in S_k} \frac{p_{k}(i,j)}{p(i,j)}
    $$
    -   $S_k$: All connected node pairs excluding $k$.
    -   $p(i,j)$: Total shortest paths between $i$ and $j$.
    -   $p_k(i,j)$: Number of those paths passing through $k$.
-   **Interpretation:** A **high betweenness** score means the node is a critical connector, controlling information flow.

---

### Katz Prestige
-   **Definition:** A node's prestige is influenced by the prestige of its neighbors, inversely proportional to their number of connections (degree).
-   **Formula (recursive):**
    $$
    P(i) = \sum_{j \in N(i)} \frac{P(j)}{\text{degree}(j)}
    $$
    -   $N(i)$: Neighbors of node $i$.
-   **Key Idea:** Connecting to prestigious nodes makes a node prestigious, but the impact is **diluted** if those prestigious nodes have many connections. This highlights that being connected to a highly connected node is less impactful than being connected to an equally prestigious but less connected node.
-   **Solution:** Typically solved using **linear algebra** (system of equations).

---

## Financial Network Analysis (Volatility Spillovers) 📈

-   **Total Volatility (for a bank $i$):**
    $$
    \sigma_i^2 = \text{High-Low-Close-Open (HLCO) volatility estimator}
    $$
-   **Variance Decomposition:**
    -   $\theta_{ij}(h)$: Effect of bank $j$ on bank $i$'s $h$-step-ahead volatility.
    -   **Proportional Influence ($C_{j \rightarrow i}$):** Measures the relative contribution of bank $j$'s volatility to bank $i$'s total volatility.
        $$
        C_{j \rightarrow i} = \frac{\theta_{ij}(h)}{\sum_j \theta_{ij}(h)}
        $$

### Key Metrics in Volatility Spillovers:

-   **Directional Connectedness (To $i$): $C_{i}^\text{in}$**
    -   Measures the total **inflow of volatility** to bank $i$ from all other banks.
    -   $$
        C_{i}^\text{in} = \sum_{j \neq i} C_{j \rightarrow i}
        $$
-   **Directional Connectedness (From $i$): $C_{i}^\text{out}$**
    -   Measures the total **outflow of volatility** from bank $i$ to all other banks.
    -   $$
        C_{i}^\text{out} = \sum_{j \neq i} C_{i \rightarrow j}
        $$
-   **System-Wide Connectedness:**
    -   Represents the overall interconnectedness of the financial system.
    -   $$
        \text{Average of all } C_{i}^\text{in} \text{ across nodes}
        $$
    -   **Insight:** During crises, system-wide connectedness often **increases**, indicating a higher risk of contagion.

---

## Key Insights & Applications 💡

-   **Medici Family Case Study:** Demonstrated the power of these metrics, showing the Medici family had the **highest betweenness and Katz prestige**, mathematically confirming their historical influence.
-   **Bank Volatility Spillovers:** Highlighted that banks in **North America and Europe dominate volatility spillovers**. System-wide connectedness significantly **increases during financial crises**.

---

## Why It Matters 🤔

These mathematical tools provide a quantitative way to **measure influence and systemic risk** in complex networks. They help uncover hidden patterns and understand the dynamics of interconnected systems, from historical power structures to modern financial markets.

[[W1L2 - Stable Matching Algorithm]]