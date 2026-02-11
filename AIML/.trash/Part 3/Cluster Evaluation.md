
Unsupervised cluster evaluation assesses the quality of clustering results **without using external labels** (since true groupings are unknown). Three key concepts - **cohesion**, **separation**, and the **Silhouette Coefficient** - are commonly used to evaluate how well a clustering algorithm (like K-Means) has grouped the data.

### 1. Cohesion
- **Definition**: Measures how tightly packed or similar the points within a single cluster are.
- Cohesion is typically quantified by the **Within Cluster Sum of Squared Errors (SSE)**:
  $$
  \text{SSE} = \sum_{i=1}^{k} \sum_{\mathbf{x} \in C_i} \|\mathbf{x} - \boldsymbol{\mu}_i\|^2
  $$
  where:
  - $k$ = number of clusters,
  - $C_i$ = the i-th cluster,
  - $\boldsymbol{\mu}$ = centroid of cluster $C_i$,
  - $\|\mathbf{x} - \boldsymbol{\mu}_i\|^2$ = squared Euclidean distance from point $\mathbf{x}$ to its cluster centroid.
- **Interpretation**: Lower SSE → higher cohesion → better clustering (within-cluster compactness).
### 2. Separation
- **Definition**: Measures how distinct one cluster is from others—i.e., how far apart different clusters are.
- Separation is quantified by **Between-Cluster Sum of Squares (BCSS)**. Compute distances between cluster centroids or between all pairs of points in different clusters. 
    $$
    \text{SSB} = \sum_{i=1}^{k} n_i \|\boldsymbol{\mu}_i - \boldsymbol{\mu}\|^2
    $$
    where $n_i$ is the size of cluster $C_i$, and $\boldsymbol{\mu}$ is the global centroid.
- **Interpretation**: Higher separation → clusters are more distinct → better clustering.

> $$SSB + SSE = \text {Constant}$$
### 3. Silhouette Coefficient
- **Purpose**: Combines both cohesion and separation into a single score ***per data point**,* then averaged over the whole dataset.
- **For a single point \(x\)**:
	- Let \(a(x)\) = average distance from \(x\) to all other points in its **own** cluster (measures **cohesion**).
	- Let \(b(x)\) = smallest average distance from \(x\) to points in any **other** cluster (measures **separation**).
	- Silhouette coefficient for \(x\):
$$    s(x) = \frac{b(x) - a(x)}{\max\{a(x), b(x)\}}
    $$
- **Range**: $-1 \leq s(x) \leq 1$
	  - $s(x) \approx 1$: Point is well-clustered (close to own cluster, far from others).
	  - $s(x) \approx 0$: Point is on the boundary between clusters.
	  - $s(x) \approx -1$: Point may be assigned to the wrong cluster.
- **Overall clustering quality**: Average \(s(x)\) across all points. Higher average → better-defined clusters.
### Practical Use
- **Choosing \(k\) in K-Means**: Plot average silhouette score vs. \(k\); pick \(k\) with highest score.
- **Comparing algorithms**: Silhouette provides a standardized way to compare different clustering results on the same data.

These internal metrics are essential when ground truth labels are unavailable. common in real-world unsupervised learning scenarios.

> [!example]
> 
> Suppose we have 4 data points in 2D space:
> 
> | Point | Coordinates | Assigned Cluster |
> |-------|-------------|------------------|
> | A     | (2, 2)      | Cluster 1        |
> | B     | (3, 3)      | Cluster 1        |
> | C     | (8, 8)      | Cluster 2        |
> | D     | (9, 9)      | Cluster 2        |
> 
> We’ll use **Euclidean distance**:  
> $$ d((x_1,y_1), (x_2,y_2)) = \sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2} $$
> 
> ### 🔢 Step 1: Compute all pairwise distances
> We’ll need these for averages:
> - $d(A,B) = \sqrt{(2-3)^2 + (2-3)^2} = \sqrt{1 + 1} = \sqrt{2} \approx 1.414$
> - $d(A,C) = \sqrt{(2-8)^2 + (2-8)^2} = \sqrt{36 + 36} = \sqrt{72} \approx 8.485$
> - $d(A,D) = \sqrt{(2-9)^2 + (2-9)^2} = \sqrt{49 + 49} = \sqrt{98} \approx 9.899$
> - $d(B,C) = \sqrt{(3-8)^2 + (3-8)^2} = \sqrt{25 + 25} = \sqrt{50} \approx 7.071$
> - $d(B,D) = \sqrt{(3-9)^2 + (3-9)^2} = \sqrt{36 + 36} = \sqrt{72} \approx 8.485$
> - $d(C,D) = \sqrt{(8-9)^2 + (8-9)^2} = \sqrt{1 + 1} = \sqrt{2} \approx 1.414$
> 
> ### 📌 Step 2: Compute \( a(x) \) and \( b(x) \) for each point
> #### ✅ Point A (in Cluster 1)
> - **Cluster 1 members**: A, B → size = 2
> - **a(A)** = average distance to other points in **same cluster**:
>   $$
>   a(A) = \frac{1}{1} \cdot d(A,B) = 1.414
>   $$
> 
> - **Distances to Cluster 2 (C, D)**:
>   - To C: 8.485
>   - To D: 9.899
>   - Average to Cluster 2: $\frac{8.485 + 9.899}{2} = \frac{18.384}{2} = 9.192$
> - Only one other cluster →  
>   $$
>   b(A) = 9.192
>   $$
> - Silhouette:
>   $$
>   s(A) = \frac{b(A) - a(A)}{\max(a(A), b(A))} = \frac{9.192 - 1.414}{\max(1.414, 9.192)} = \frac{7.778}{9.192} \approx 0.846
>   $$
> 
> #### ✅ Point B (in Cluster 1)
> - **a(B)** = distance to A = 1.414
> - **Distances to Cluster 2**:
>   - To C: 7.071
>   - To D: 8.485
>   - Average = $\frac{7.071 + 8.485}{2} = \frac{15.556}{2} = 7.778$
> - So $b(B) = 7.778$
> - Silhouette:
>   $$
>   s(B) = \frac{7.778 - 1.414}{\max(1.414, 7.778)} = \frac{6.364}{7.778} \approx 0.818
>   $$
> #### ✅ Point C (in Cluster 2)
> - **a(C)** = distance to D = 1.414
> 
> - **Distances to Cluster 1 (A, B)**:
>   - To A: 8.485
>   - To B: 7.071
>   - Average = $\frac{8.485 + 7.071}{2} = 7.778$
> - So $b(C) = 7.778$
> - Silhouette:
>   $$
>   s(C) = \frac{7.778 - 1.414}{7.778} = \frac{6.364}{7.778} \approx 0.818
>   $$
> #### ✅ Point D (in Cluster 2)
> - **a(D)** = distance to C = 1.414
> 
> - **Distances to Cluster 1**:
>   - To A: 9.899
>   - To B: 8.485
>   - Average = $\frac{9.899 + 8.485}{2} = 9.192$
> - So $b(D) = 9.192$
> - Silhouette:
>   $$
>   s(D) = \frac{9.192 - 1.414}{9.192} = \frac{7.778}{9.192} \approx 0.846
>   $$
> ### 📊 Step 3: Compute overall Silhouette Coefficient
> Average all individual silhouette scores:
> $$
> \text{Average } s = \frac{s(A) + s(B) + s(C) + s(D)}{4} = \frac{0.846 + 0.818 + 0.818 + 0.846}{4}
> = \frac{3.328}{4} = 0.832
> $$


---

Unsupervised measures for cluster validity
Cohesion
SSE

Separation
SSB

TSS = SSE + SSB

Silhouette coefficient

Similarity and proximity matrix => correlation matrix

Clustering tendency -> finding whether there are clusters in the data without having to cluster. Done by conducting tests to check randomness. Less randomness -> perhaps there are clusters. Ex: Hopkins statistic


Supervised measures for cluster validity
helps know how good a clustering algorithm is to the ground truth
Classif oreint & similarity oreint

Classification oriented
Entropy
Purity
Precision
Recall
F Measure

Similarity oriented
rand statistic (SMC) and jaccard coefficient
Key: rand statistic and jaccard coeff directly link to binary variables. Why?
Because when we try to find how good a clustering algorithm is wrt to actual labels, we're calculating how similar our clustering is to the actual labels. So we calculate how much our clustering got right and got wrong etc. this is the exact same as a binary variable.


