Comparing how good the clustering is w.r.t the actual grouping of data
- We have access to class labels here

Done as:
- Classification oriented -> How well do the clusters match up with the classes
	- How similar is current clustering with the ideal clustering
	- Ideal clustering is when the the classes are perfectly partitioned
- Similarity oriented -> How similar is our clustering with the actual classes
	- Calculating correlation between ideal similarity matrices

## Classification oriented
**Entropy**: The degree to which each cluster consists of objects of a single class. For each cluster, the class distribution of the data is calculated first, i.e., for cluster $j$ we compute $p_{ij}$, the probability that a member of cluster $i$ belongs to class $j$ as $$p_{ij} = m_{ij}/m_i$$, where $m_i$ is the number of objects in cluster $i$ and $m_{ij}$ is the number of objects of class $j$ in cluster $i$. Using this class distribution, the entropy of each cluster $i$ is calculated using the standard formula, $$e_i = -\sum_{j=1}^{L} p_{ij} \log_2 p_{ij}$$, where $L$ is the number of classes. The total entropy for a set of clusters is calculated as the sum of the entropies of each cluster weighted by the size of each cluster, i.e., $$e = \sum_{i=1}^{K} \frac{m_i}{m} e_i$$, where $K$ is the number of clusters and $m$ is the total number of data points.


---
**Purity**: Another measure of the extent to which a cluster contains objects of a single class. Using the previous terminology, the purity of cluster $i$ is $$p_i = \max_j p_{ij}$$the overall purity of a clustering is $$\text{purity} = \sum_{i=1}^{K} \frac{m_i}{m} p_i$$

---
**Precision**: The fraction of a cluster that consists of objects of a specified class. The precision of cluster $i$ with respect to class $j$ is $$\text{precision}(i,j) = p_{ij}$$

---
**Recall**: The extent to which a cluster contains all objects of a specified class. The recall of cluster $i$ with respect to class $j$ is $$\text{recall}(i,j) = m_{ij}/m_j$$where $m_j$ is the number of objects in class $j$.

---
**F-measure**: A combination of both precision and recall that measures the extent to which a cluster contains *only* objects of a particular class and *all* objects of that class. The F-measure of cluster $i$ with respect to class $j$ is  
$$
F(i,j) = \frac{2 \times \text{precision}(i,j) \times \text{recall}(i,j)}{\text{precision}(i,j) + \text{recall}(i,j)}.
$$



## Similarity oriented
### Treating as binary variables.
Draw the contingency table for these cases:
![[Pasted image 20260115175330.png]]
Compute Jaccard Measure or Rand statistic (SMC) to compare how similar our clustering result is to the actual true result

> Because when we try to find how good a clustering algorithm is wrt to actual labels, we're calculating how similar our clustering is to the actual labels. So we calculate how much our clustering got right and got wrong etc. this is the exact same as a binary variable.

Done with ideal cluster similarity matrix and ideal class similarity matrix.
- Ideal cluster matrix is similarity of points when clustering is idea. ideal class matrix is similarity in ideal case where cluster mirrors the classes

> [!example]
> To Compute the **correlation between ideal cluster similarity matrix and ideal class similarity matrix**
>
> ### ✅ **Step 1: Ideal Similarity Matrices**
>
> **Ideal class similarity matrix** (based on true labels: {A,B,E} in class 0; {C,D,F} in class 1):
> ```
>    A B C D E F
> A [1 1 0 0 1 0]
> B [1 1 0 0 1 0]
> C [0 0 1 1 0 1]
> D [0 0 1 1 0 1]
> E [1 1 0 0 1 0]
> F [0 0 1 1 0 1]
> ```
>
> **Ideal cluster similarity matrix** (based on clustering: {A,B,E} in cluster 0; {C,D} in cluster 1; {F} in cluster 2):
> ```
>    A B C D E F
> A [1 1 0 0 1 0]
> B [1 1 0 0 1 0]
> C [0 0 1 1 0 0]
> D [0 0 1 1 0 0]
> E [1 1 0 0 1 0]
> F [0 0 0 0 0 1]
> ```
>
> ### 📊 **Step 2: Vectorize Upper Triangle**
> Extract the upper triangle (excluding diagonal) from each matrix:
> - `ideal_class_vec` = `[1, 0, 0, 1, 0, 0, 0, 1, 0, 1, 0, 1, 0, 1, 0]`
> - `ideal_cluster_vec` = `[1, 0, 0, 1, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0]`
>
> ### 📈 **Step 3: Compute Pearson Correlation**
> Using the formula:
> $$
> r = \frac{\text{cov}(X, Y)}{\sigma_X \sigma_Y}
> $$
> The correlation between the two vectors is:
> - **Correlation (ideal class vs. ideal cluster)** = **0.739**