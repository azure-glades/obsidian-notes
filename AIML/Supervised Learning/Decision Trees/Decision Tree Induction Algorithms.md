**Decision Tree Induction** is the process of learning a classification or regression model from a dataset by constructing a tree-like structure. It is a "top-down, greedy" approach that breaks down a complex decision-making process into a series of simpler, hierarchical rules.
# Hunt’s Algorithm
Hunt’s Algorithm grows a tree recursively by partitioning training records into successively "purer" subsets. Actual algorithms implement hunt's with some changes.

> [!tldr] Algorithm
> Let $D_t$ be the set of training records that reach node $t$. The steps are as follows:
> #### 1. Termination (Pure Class)
> If all records in $D_t$ belong to the same class $y_j$, then $t$ is a **leaf node** labeled as $y_j$. The recursion for this branch stops here.
> #### 2. Splitting (Mixed Classes)
> If $D_t$ contains records that belong to more than one class, an **attribute test condition** is selected to partition the records into smaller subsets.
> - A child node is created for each outcome of the test.
> - The records in $D_t$ are distributed to the children based on the outcomes.
> - The algorithm is then **recursively applied** to each child node.
> #### 3. Handling Special Cases
> - **Empty Subset:** If a test outcome results in a subset that is empty (no records), the child node is created as a leaf node labeled with the **majority class** of the parent node $D_t$.
> - **Identical Attributes:** If all records in $D_t$ have identical attribute values but belong to different classes, it is impossible to split further. In this case, $t$ is made a leaf node labeled with the **majority class** of the records in $D_t$.

# ID3 (Iterative Dichotomizer 3) Algorithm
This algorithm builds a decision tree **top-down**, using a **greedy approach** (choosing the best attribute at each step) and **never revisits** a split once made. It assumes the data is **discrete** (non-continuous) and free of missing values (basic version).
- It uses *information gain*

> [!summary] Algorithm
> 1. **Start with the full dataset as the root node.**
> 2. **Check for base cases**:
>     - If all examples belong to the same class, create a leaf node with that class label.
>     - If there are no features left to split on but examples still belong to multiple classes, create a leaf node with the majority class.
> 3. **Calculate the entropy of the current dataset.**
> 4. **For each unused attribute**, calculate the **information gain** resulting from splitting on that attribute.
> 5. **Select the attribute with the highest information gain** as the splitting criterion for the current node.
> 6. **Split the dataset** into subsets based on the values of the selected attribute.
> 7. **Recursively apply the algorithm** to each subset, creating child nodes.
> 8. **Return the resulting decision tree**.

```al
ALGORITHM ID3(Examples, Target_Attribute, Attributes)
    // Create a Root node
    Root = CreateNode()

    // Base Case 1: All examples belong to the same class
    If all examples in Examples have the same Target_Value:
        Return Root with Label = Target_Value

    // Base Case 2: No more attributes to split on
    If Attributes is empty:
        Return Root with Label = most common Target_Value in Examples

    // Step: Choose the best attribute
    A = Attribute from Attributes with highest Information Gain
    Root.Decision_Attribute = A

    // Step: Create branches for each value of the chosen attribute
    For each unique value 'v' of A:
        Add a new branch below Root for (A = v)
        Examples_v = subset of Examples where A == v

        If Examples_v is empty:
            // Handle empty partitions
            Add a leaf node with Label = most common Target_Value in Examples
        Else:
            // Recursive call: Remove used attribute A from the list
            Add subtree = ID3(Examples_v, Target_Attribute, Attributes - {A})
RETURN Root
```

# C4.5 Algorithm
The **C4.5 algorithm** is an extension of the **ID3 algorithm** developed by Ross Quinlan. 
- Uses **gain ratio** instead of information gain.
- Handles **continuous attributes** via thresholding.
- Supports **missing attribute values**.
- Includes **tree pruning** to enhance generalization.

> [!tldr] Algorithm
> 1. **Start with the full training dataset as the root node.**
> 2. **Check stopping conditions (base cases):**
>    - If all instances in the current node belong to the same class, create a **leaf node** labeled with that class.
>    - If there are no attributes left to split on (or no informative attributes), create a **leaf node** labeled with the **majority class** of the instances in that node.
> 3. **Preprocess attributes:**
>    - **For continuous attributes**: Sort their values and consider possible thresholds (midpoints between adjacent distinct values) to create binary splits.
>    - **For missing values**: Handle them during the splitting process by distributing instances probabilistically or ignoring them in gain calculations.
> 4. **Compute the gain ratio for each candidate attribute**
> 	- **Select the attribute with the highest gain ratio** as the splitting criterion for the current node.
> 5. **Partition the dataset** based on the selected attribute:
> 	- For **discrete attributes**: Create one branch for each possible value.
> 	- For **continuous attributes**: Create two branches (≤ threshold and > threshold).
> 6. **Handle missing values during partitioning**:
> 	- Instances with missing values for the splitting attribute are assigned to all branches with weights proportional to the size (or probability) of each branch.
> 7. **Recursively apply the algorithm** to each resulting subset (child node) using the remaining attributes.
> 8. ***Optional***: After the full tree is built, perform post-pruning (using techniques like error-based pruning) to avoid overfitting:
>    - Evaluate whether replacing a subtree with a leaf node improves or maintains accuracy on validation data (or estimated error).
>    - Prune subtrees if they do not contribute significantly to classification accuracy.
> 9. **Return the final pruned decision tree.**

# CART (Classification and Regression Trees) Algorithm
The **CART (Classification and Regression Trees)** algorithm, developed by Breiman, Friedman, Olshen, and Stone, is a powerful and widely used decision tree learning method. It can be used for both **classification** (predicting class labels) and **regression** (predicting continuous values).

> [!tldr] Algorithm
> 1. **Start with the entire training dataset as the root node.**
> 2. **Check stopping criteria (base cases):**
> 	   - If all instances in the node belong to the same class (for classification) or have the same target value (for regression), mark it as a **leaf node**.
> 	   - If the number of instances in the node is below a predefined minimum (e.g., `min_samples_split`), create a **leaf node**.
> 	   - If no further split leads to a significant improvement (e.g., below a threshold in impurity reduction), stop splitting.
> 3. **Evaluate all possible binary splits:**
> 	   - **For numerical features**: Consider every possible threshold (typically midpoints between sorted unique values) to split the data into two groups: $( x \leq t )$ and $( x > t )$.
> 	   - **For categorical features**: CART only considers **binary splits**, so it evaluates all possible ways to partition the categories into two disjoint subsets (or uses efficient heuristics in practice).
> 4. **Choose the best split using an impurity measure:**
> 	   - **For classification**: Use **Gini impurity** (most common in CART), though entropy or misclassification error can also be used.
> 	   - **For regression**: Use **Mean Squared Error (MSE)** or **Mean Absolute Error (MAE)** as the impurity measure.
> 	   - Compute the **weighted impurity reduction** (also called gain) for each candidate split: $$
>      \Delta \text{Impurity} = \text{Impurity}_{\text{parent}} - \left( \frac{N_{\text{left}}}{N} \cdot \text{Impurity}_{\text{left}} + \frac{N_{\text{right}}}{N} \cdot \text{Impurity}_{\text{right}} \right)
>      $$
> 5. **Select the split (feature + threshold or partition) that maximizes impurity reduction** (i.e., minimizes weighted impurity).
> 6. **Split the current node into two child nodes** based on the best binary split.
> 	- If the attribute has many classes, group the classes together and find the best binary split.
> 	- Ex: For attribute `Weather(Sunny, Windy, Rainy)` group it into all possibilities of split, i.e `(Sunny+Windy, Rainy) ; (Sunny, Windy+Rainy) ; (Sunny+Rainy, Windy)` and find the split with lowest impurity.
> 7. **Recursively apply steps 2–6 to each child node** until stopping criteria are met.
> 8. **Return the final (pruned) decision tree.**

# Differences

| Feature / Aspect                   | **ID3**                                    | **C4.5**                                                           | **CART**                                                      |
| ---------------------------------- | ------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------- |
| **Task Type**                      | Classification only                        | Classification only                                                | **Both classification and regression**                        |
| **Split Type**                     | Multi-way splits (one per attribute value) | Multi-way splits                                                   | **Binary splits only**                                        |
| **Attribute Types**                | **Discrete (categorical) only**            | **Discrete and continuous**                                        | **Discrete and continuous**                                   |
| **Handling Continuous Attributes** | ❌ Not supported                            | ✅ Yes (uses thresholds to binarize)                                | ✅ Yes (uses optimal threshold splits)                         |
| **Handling Missing Values**        | ❌ Not supported                            | ✅ Yes (uses probabilistic distribution)                            | ⚠️ Limited (often handled via surrogate splits or ignored)    |
| **Splitting Criterion**            | **Information Gain**                       | **Gain Ratio** (to reduce bias toward high-cardinality attributes) | **Gini Impurity** (classification), **MSE/MAE** (regression)  |
| **Pruning**                        | ❌ No pruning                               | ✅ **Post-pruning** (error-based)                                   | ✅ **Cost-complexity (post-)pruning**                          |
| **Tree Structure**                 | Unpruned, multi-way tree                   | Pruned, multi-way tree                                             | Pruned (optional), **strictly binary tree**                   |
| **Bias Toward Attributes**         | Biased toward attributes with many values  | Reduced bias due to gain ratio                                     | Less biased (Gini doesn’t favor many splits)                  |
| **Output**                         | Decision tree (unpruned)                   | Decision tree (pruned)                                             | Decision tree (pruned, binary)                                |
| **Use in Ensembles**               | Rarely                                     | Rarely                                                             | ✅ **Commonly used** (e.g., Random Forests, Gradient Boosting) |
