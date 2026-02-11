
The "type" of a cluster is defined by the criteria used to determine if points belong together.
This overview details the primary definitions and characteristics of different cluster types used in data mining and pattern recognition.
## 1. Well-Separated Clusters 
- **Definition:** A cluster is a set of objects where each object is closer (or more similar) to every other object in the cluster than to any object outside the cluster.
- **Key Characteristics:**
    - Often involves a threshold for closeness or similarity.
    - Clusters can be non-globular and take any shape.
![[Pasted image 20260111165449.png]]
## 2. Prototype-Based / Center-Based Clusters
- **Definition:** A cluster is a set of objects where each object is closer to the **prototype** of the cluster than to the prototype of any other cluster.
- **Prototypes:**
    - **Centroid:** The mean of all points in the cluster (used for continuous data).
    - **Medoid:** The most representative point in the cluster (used for categorical data).
- **Key Characteristics:**
    - Clusters are typically globular (spherical).
![[Pasted image 20260111165501.png]]
## 3. Graph-Based Clusters / Contiguity-Based Clusters
- **Definition:** A cluster is a connected component in a graph representation of data.
- **Types:**
    - **Contiguity-Based Clusters:** Objects are connected if they are within a specified distance.
        - _Issue:_ Can merge distinct clusters due to noise (e.g., "noise bridges").
    - **Clique-Based Clusters:** Formed when a group of objects is completely connected.
- **Key Characteristics:**
    - Suitable for irregular or intertwined clusters.
    - Sensitive to noise.
![[Pasted image 20260111165522.png]]
## 4. Density-Based Clusters
- **Definition:** A cluster is a dense region of objects surrounded by low-density regions.
- **Key Characteristics:**
    - Effective for irregular clusters and noisy data.
    - Avoids merging clusters via noise bridges.
![[Pasted image 20260111165509.png]]
## 5. Shared-Property / Conceptual Clusters
- **Definition:** A cluster is a set of objects that share some common property.
- **Key Characteristics:**
    - Includes all previous notions of clusters (e.g., center-based, density-based).
    - Can detect complex cluster shapes (e.g., triangular, rectangular, intertwined circles).        
    - Complex notions may overlap with pattern recognition.

![[Pasted image 20260111165530.png]]

| **Clustering Type** | **Primary Strength**                                             | **Main Weakness**                                                   | **Best For**                                                        |
| ------------------- | ---------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| **Well-Separated**  | High precision; clusters are distinct and unambiguous.           | Idealistic; rarely found in real-world "noisy" datasets.            | Natural data with very clear gaps between groups.                   |
| **Prototype-Based** | Mathematically simple and computationally efficient.             | Struggles with non-globular shapes and outliers.                    | Large datasets with roughly spherical distributions.                |
| **Graph-Based**     | Can identify complex, irregular, or intertwined shapes.          | Very sensitive to noise; a few points can bridge distinct clusters. | Intertwined data where points are physically connected.             |
| **Density-Based**   | Robust against noise and outliers; finds arbitrary shapes.       | Difficulties with datasets that have varying levels of density.     | Irregularly shaped clusters in noisy environments.                  |
| **Conceptual**      | Extremely flexible; can find clusters based on high-level logic. | Highly dependent on how well the "concept" is defined.              | Complex patterns (e.g., specific shapes like triangles or circles). |