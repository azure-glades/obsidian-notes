This video, the tenth lecture in the NPTEL course "Artificial Intelligence for Economics" by Addoi Mitro, Assistant Professor at IIT Kharagpur, shifts focus from heuristic search and optimization to **data-driven models and machine learning**. Specifically, this lecture introduces **unsupervised learning**, with a deep dive into **clustering and segmentation**.

---

### Essential Topics and Key Points:

The lecture covers the following essential topics and key points:

---

### 1. Introduction to Unsupervised Learning

- **Definition:** Unsupervised learning deals with **unlabeled data**, meaning observations are provided without any predefined categories or labels. The goal is to discover hidden patterns or structures within the data.
    
- **Analogy:** The lecturer uses the example of a child shown pictures of various animals without being told their names. The child can still group similar-looking animals based on shared features (stripes, horns, body shape), demonstrating an intuitive form of clustering.
    

---

### 2. What is Clustering?

- **Intuitive Definition:** Clustering involves grouping observations (data points) that are similar to each other into distinct sets called **clusters**.
    
- **Feature-Based Representation:** To perform clustering, data points are represented as **feature vectors** in a **feature space**. For example, in the income and expenditure example, each person is a 2D vector (income, expenditure), plotted as a point in a 2D space.
    
- **High-Density Regions:** Clusters are essentially **high-density regions of points** in the feature space.
    
- **Formal Definition (Proximity-Based):**
    
    - Requires a **notion of closeness or distance** between data points.
        
    - **Distance Measures:**
        
        - **Euclidean Distance:** Most common for continuous real-valued feature spaces.
            
        - **Hamming Distance:** Used for binary feature vectors.
            
        - Other measures: Mahalanobis distance, Manhattan distance. (For this course, Euclidean distance is primarily used).
            
    - **Cluster Criteria:** A valid cluster is a subset of observations where:
        
        - **Mean Intra-cluster Distance is Low:** Points within the same cluster are close to each other.
            
        - **Mean Inter-cluster Distance is High:** Points from different clusters are far apart from each other.
            

---

### 3. Agglomerative Clustering

- **Approach:** This is a **bottom-up** or **hierarchical** clustering method.
    
- **Initialization:** Each data point initially starts as its own individual cluster.
    
- **Merging Strategy:** The algorithm iteratively **merges pairs of the closest clusters** until no further mergers are possible (based on a predefined distance threshold).
    
- **Linkage Criteria (How to measure distance between clusters):**
    
    - **Single Linkage (Minimum Distance):** The distance between two clusters is defined as the minimum distance between any two points, one from each cluster. (Lenient: Clusters are considered close if even just one pair of points is close).
        
    - **Complete/Multiple Linkage (Maximum Distance):** The distance between two clusters is the maximum distance between any two points, one from each cluster. (Strict: Clusters are considered far apart if even just one pair of points is far).
        
    - **Average Linkage (Mean Distance):** The distance between two clusters is the average distance between all possible pairs of points, one from each cluster.
        
- **Termination:** The process stops when no more clusters can be merged (i.e., all remaining inter-cluster distances exceed the specified threshold).
    
- **No Pre-specified K:** A key characteristic is that the number of final clusters (`K`) is **not** pre-specified; it's determined by the chosen distance threshold.
    

---

### 4. K-Means Clustering

- **Approach:** This is a **prototype-based** or **partitioning** clustering algorithm.
    
- **Pre-specified K:** Unlike agglomerative clustering, K-means requires the user to **pre-specify the number of clusters (K)** they want to create.
    
- **Cluster Prototypes (Centroids/Means):** Each cluster is represented by a **cluster mean** (or centroid), which is the mean feature vector of all points assigned to that cluster.
    
- **Algorithm Steps:**
    
    1. **Initialization:** Randomly choose `K` data points to be the initial cluster centers (prototypes).
        
    2. **Cluster Assignment:** Assign each of the remaining data points to the **closest cluster center** (based on Euclidean distance).
        
    3. **Centroid Recalculation:** Recalculate the cluster centers by taking the mean of all data points currently assigned to each cluster.
        
    4. **Iteration:** Repeat steps 2 and 3 until a stopping criterion is met.
        
- **Stopping Criteria (Convergence):**
    
    - No further change in cluster assignments of any data point.
        
    - No significant change in the cluster centers (prototypes).
        
    - Mean intra-cluster distance reaches a local minimum (not reducing further).
        
- **Limitations:**
    
    - **Local Optima:** K-means is only guaranteed to find a **local optimum**, not necessarily the global best clustering.
        
    - **Sensitivity to Initialization:** The final clustering result can depend heavily on the initial random choice of cluster centers.
        
    - **Empirical Choice of K:** There's no fixed rule for choosing the optimal `K`. Practitioners often run K-means for multiple `K` values and plot the mean intra-cluster distance (or a similar metric) to find an "elbow point" where increasing `K` yields diminishing returns in reducing intra-cluster distance.
        

---

### 5. Applications in Economics

- **Market Segmentation:** Grouping customers based on attributes like age, gender, demographics, income, or spending habits. This helps companies target specific groups with tailored products or marketing strategies.
    
- **Economic Policy and Design/Analysis:** Clustering countries, regions, or localities based on socio-economic characteristics (GDP, employment rates, infrastructure, income levels) to understand the impact of policies or design targeted interventions.
    
- **Labor Market Analysis:** Grouping workers based on skills, educational experience, and other factors to better match jobs with suitable candidates or to identify skill gaps.
    

---

The lecture concludes by reiterating the core concepts of clustering and looking forward to discussing more data-driven methods for knowledge extraction and prediction in future lectures.