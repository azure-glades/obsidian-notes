
[[K Means Clustering]]
[[Bisecting K Means]]

| **Feature**            | **K-Means (Partitional)** | **Hierarchical**                 | **DBSCAN (Density-Based)**  |
| ---------------------- | ------------------------- | -------------------------------- | --------------------------- |
| **Shape**              | Globular/Spherical        | Any shape (depending on linkage) | Irregular/Arbitrary         |
| **Outliers**           | Sensitive (affects mean)  | Handles somewhat                 | Excellent at ignoring noise |
| **Number of Clusters** | Must specify $K$ upfront  | Determined by cutting the tree   | Determined automatically    |
