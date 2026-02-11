While standard K-Means tries to find all $K$ clusters at once (which can be messy if the random starting points are bad), **Bisecting K-Means** takes a "divide and conquer" approach.

> [!tldr] Bisecting K Means Algorithm
> Bisecting K-Means is a **top-down** approach.
> 1. **The "Global" Cluster:** Start with every data point in one giant cluster.
> 2. **The Split:** Pick a cluster and split it into **exactly two** sub-clusters using the standard K-Means algorithm (with $K=2$).
>     - _Note:_ Because you are only ever running $K=2$, the algorithm is much more stable and less likely to get confused by random initialization.
> 3. **The Selection:** Look at your current clusters and decide which one to split next.
> 4. **Repeat:** Keep splitting until you have reached your desired number of $K$ clusters.
> ![[Pasted image 20260111181206.png]]


Selection strategy
- **Highest  SSE:** Pick the cluster with the highest **Sum of Squared Errors**. Reduces overall SSE and entropy
- **Largest Size:** Pick the cluster with the most points. Produces clusters of similar density

## Advantage of Bisecting K Means
Standard K-Means is sensitive to where the initial centroids are placed. If they start in a bad spot, you get bad clusters. Bisecting K-Means is much more **robust** because it performs multiple trials of $K=2$ splits and chooses the best one, making it less likely to get stuck in a poor configuration.