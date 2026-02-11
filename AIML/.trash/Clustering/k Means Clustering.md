Reference book : Pearson Machine Learning - Saikat Dutt, S Chandramouli

```al
ALGORITHM kMeans(data, k)
//INPUT: hyperparameter k - no. of clusters
	Select k random points in data-space
	WHILE (SSE > threshold OR centroids dont change)
		Assign each point in data to nearest centroid
		Measure distance of each point in cluster from the centroid
		Calculate SSE
		Move the centroids of the cluster based on the distance and SSE
	END-WHILE
RETURN clusters
```

Homogenity of a cluster is calculated as WCSS (Within cluster sum of squares) i.e Sum of squares error (SSE)
Hyperparameter k determines the no. of clusters.
For small datasets, in general $k = \sqrt{n/2}$ 

Elbow method - to find ideal k value
1. Run k means on different values of k (suppose from 2 to 20)
2. Calculate WCSS error for all iterations
3. Plot k vs WCSS
4. The elbow-point -> point where the WCSS curve flattens -> Not much improvement in WCSS for a given no of clusters

