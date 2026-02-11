The **K-means algorithm** is a popular **unsupervised** machine learning method used for **clustering** - that is, grouping similar data points together.
### Key points
- **Objective**: Minimize the **within-cluster sum of squares (WCSS)** - the total squared distance of points to their cluster centroids.
- **Assumptions**: Clusters are spherical and of similar size; sensitive to scale, so **feature scaling** (e.g., standardization) is often needed.
- $K$ is a *hyperparameter* that is determined with a validation set through elbow method

The algorithm follows an iterative process often referred to as **Lloyd's Algorithm**.

> [!tldr] Lloyd's Algorithm
> 1. **Initialization:** You pick a number ($K$) of starting points. These are called **centroids** (the "centers" of your clusters). Usually, these are just random points from your dataset.
> 2. **Assignment:** Every single data point looks at the $K$ centroids and asks, "Which one am I closest to?" Each point joins the cluster of its nearest centroid.
> 3. **Update:** Now that we have groups, the centroids move. We calculate the **average (mean)** of all the points in a cluster. The centroid jumps to that new average position.
> 4. **Repeat:** We do steps 2 and 3 over and over. Each time, the centroids move to a better "middle" spot, and points might switch groups to stay with their closest center. We stop when the centroids stop moving.
![[Pasted image 20260111170046.png]]
### **Time Complexity:** $O(n \cdot K \cdot I \cdot d)$
Where n is no of points, K is no of clusters, I is no of iterations and d is no of attributes. kMeans is linear
### **Space Complexity:** $O((n+K)d)$
Where n is no of points, K is no of clusters, d is no of attributes
### Objective/Loss function
K means tries to minimize **Within cluster sum of squares (WCSS) or Sum of squares error (SSE)**. This is the distance between a point ($x$) and its assigned centroid ($m$).
Square -> penalizes larger distances more heavily
$$\text{ Within cluster sum of squares error } = \sum_{i=1}^{K} \sum_{x \in C_i} \text{dist}(x, m_i)^2$$

- **Inner Sum:** Adds up the squared distances of all points in one cluster to their center.
- **Outer Sum:** Adds those totals together for all $K$ clusters.

Low SSE -> the points are huddled very tightly around their centroids -> **compact, circular clusters**.
High SSE -> the points are too widely spread out -> clusters are wide and less dense, being more irregular

Distance function can be euclidean, cosine similarity etc.

## Initial centroid problem
Since centroids are chosen by random, the inital selection of centroids determines the performance of the algorithm.
- By sheer probabilty, if all initial centroids arent well distributed such that 2 or more end up the same cluster, we end up with a false split across clusters.

**The Trap:** Poor selection of initial centroids can lead the algorithm to get stuck in a **local minimum** rather than finding the **global minimum**

**Probability:** As K increases, the probability of randomly picking one centroid from each "real" cluster drops drastically.
- This leads to splitting natural clusters or merging distinct one

### Other problems
1. K means assumes clusters to be globular, so it fails on non-globular clusters. 
2. Outliers often distort clusters or shift the centroids

### Solutions
- Multiple runs
- Sample and use hierarchical clustering to determine initial centroids
- Initialize more than k centroids and then select the best k
- Pre-processing - eliminate outliers and normalize data
- Post-processing - Eliminate small clusters which may be outliers
- Split clusters with high SSE.
- Merge close clusters with low SSE

- [[Bisecting K Means]]  - incremental partitioning of data
- K means++ - alternate initial centroid selection method

# K Means ++
Instead of pure randomness, **spread out the initial centroids** using a **probabilistic, distance-based strategy**

> [!tldr] K Means++
> 1. **Pick the first centroid** uniformly at random from the data points.
> 2. For each remaining data point, compute its **distance squared** $D(x)^2$ to the **nearest centroid already chosen**.
> 3. **Select the next centroid** with probability proportional to $D(x)^2$
>     - Points **far from existing centroids** are **more likely** to be chosen.
> 4. Repeat steps 2–3 until you have **K initial centroids**.
> 5. Proceed with standard K-Means using these smartly placed seeds.

This is called **“probability proportional to squared distance”** sampling.
- Encourages centroids to be **well-separated** from the start.
- Reduces chance of redundant centroids in dense regions.
- **Theoretically guarantees** a much better expected solution (within a log factor of optimal).
- In practice: **faster convergence + lower final SSE**.

