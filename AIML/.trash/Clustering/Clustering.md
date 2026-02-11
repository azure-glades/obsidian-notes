Clustering is an unsupervised learning technique where the goal is to group data-points into clusters such that points in the same cluster are more similar to each other, than to points in other clusters.
- Example: Given a bunch of customer data, clustering can separate them into groups with similar buying behavior.

Imp:
- Data is unlabelled -> the L.A. finds clusters on its own
- Similarity measure is required to cluster (euclidean distance, density, connectivity etc)

Major clustering techniques:
- Partitioning methods - [[Clustering/k Means Clustering]]
- [[Hierarchical clustering]] - Agglomerative Clustering, Divisive Clustering
- Density-based methods

| Method        | Characteristic                                                                                                                                                                                                                |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Partitioning  | - Mean represents cluster center<br>- Distance-metric used<br>- Best when clusters are spherical-ish                                                                                                                          |
| Hierarchical  | - Creates a tree-like structure by decomposing large clusters<br>- Distance-metric used. Distance between same-cluster and different-cluster points is use for splitting<br>- Best when there are classes-subclasses involved |
| Density based | - Identifies dense regions in space which are separated by less-dense regions<br>- Density metrics are used -> outliers are ignored<br>- Best when clusters are of arbitrary shape                                            |
