**Clustering** ( also called *cluster analysis* or data segmentation) is a technique used to group a set of objects in such a way that:
- **Objects in the same group (called a *cluster*)** are **similar** to each other.
- **Objects in different groups** are **dissimilar** to each other.

>[!important] Definition
> A cluster is a group of points (that are similar to each other in some way)
> A clustering is a group of clusters. Different clusters are distinct

> See futher: [[Types of Clusters]] , [[Types of Clustering]]
### Goal of Clustering
A good clustering solution aims to:
- Ensure similar objects/data points are in the same cluster
- Ensure dissimilar objects/data points are in different clusters
### Considerations for Analysing clusters
- Partition criteria: Structure of final groups
	- Single-level
	- Hierarchical clusters

| Hierarchical                                                                                                                     | Partitional                                  |
| -------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------- |
| Clusters are nested and organized into a tree structure                                                                          | Divides data into non-overlapping subsets    |
| Data object belongs in its cluster and superclusters                                                                             | One data object can belong to only 1 cluster |
| Each cluster is a union of its subclusters                                                                                       |                                              |
| Root node is the largest cluster containing all data points. Internal nodes partition data until leaf nodes only have 1 cluster. |                                              |

- Separation of clusters: whether a data-point can belong to multiple clusters
	- Exclusive clusters
	- Overlapping clusters
	- Fuzzy

| Exclusive                                                            | Overlapping                                                  | Fuzzy                                                                                                         |
| -------------------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------- |
| Each data point belongs only in 1 cluster                            | Datapoints can belong in many clusters                       | Datapoints belong to all clusters to some degree                                                              |
| No overlap of clusters - Mutually exclusive                          | Clusters overlap                                             | Clusters are all spread across the complete dataset                                                           |
| Deterministic - A datapoint either fully belongs to a cluster or not | A datapoint belongs to a set of clusters                     | Stochastic - the probability that a datapoint belongs to a cluster is known (i.e grade or score, from 0 to 1) |
| Clusters are well separated                                          | A datapoint fully belongs to a cluster. No partial inclusion | The total probability of a datapoint over all the clusters is 1                                               |

- Similarity measure - This is the **mathematical logic** used to decide if two points belong together.
	- distance-based 
	- connectivity-based (density)

- Inclusion of data: Whether all data-points are grouped into clusters. Sometimes outliers are ignored
	- Complete
	- Partial

| Complete                              | Partial                                                  |
| ------------------------------------- | -------------------------------------------------------- |
| All datapoints are assigned a cluster | Some datapoints end up with no clusters assigned to them |
### Basics terms
- **Data representation**: Different types of data have different similarity measures.
- **Clustering space**: The space defined by the attributes of the data (also called *feature space* in ML).
	- Each attribute is a dimension of the clustering space
	- A data point is a vector in this clustering space

- **[[Similarity Measures]]**: A means of comparing how close 2 data points are. 
	- One can also use dissimilarity measures like distance between points.

- **[[Feature processing]]**: Processing the features to reduce noise or bias, like:
	- Feature scaling - Standardization/Normalization
	- Encoding - converting from one data type to another
	- Dimensionality reduction - PCA

- **[[Clustering algorithms]]**: Groups data points into clusters. 
	- Some algos use a hyperparameter = no. of clusters to make

- **[[Cluster Validation]]**: To quantify the goodness of clustering

### Challenges with analysing clusters
- Scalability (i.e Generalization) - Clustering should apply for entire data and not just the samples considered
- Dealing with different types of attributes
- Constraint-based clustering.
- Interpretability and usability

## Data representation
Before an algorithm can group data, it needs to be organized. There are two primary ways to represent your dataset:
### A. Data Matrix (2-Mode)
This is your standard spreadsheet format.
- **Structure:** $n$ objects (rows) $\times$ $p$ variables (columns).
- **Mode:** It is "two-mode" because the rows and columns represent different entities (objects vs. attributes).
- **When to use:** Use this when you have the raw measurements for every object (e.g., height, weight, age for 100 people).
![[Pasted image 20260105101103.png]]
### B. Dissimilarity/Distance Matrix (1-Mode)
This is a square matrix that stores the "distance" between every pair of objects.
- **Structure:** $n \text{ objects} \times n \text{ objects}$. The value at $[i, j]$ is the difference between object $i$ and object $j$.
- **Mode:** It is "one-mode" because rows and columns represent the same entity (the objects).
- **When to use:** Use this when you don't have raw attributes, but you do have a "score" of how different things are. It is the primary input for **Hierarchical Clustering**.
![[Pasted image 20260105101113.png]]
