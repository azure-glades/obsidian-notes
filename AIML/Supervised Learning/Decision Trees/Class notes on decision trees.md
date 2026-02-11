• **Supervised Learning** is an approach where an algorithm learns from **pre-existing, labeled data** (the correct solutions) to infer a function that can map new, unseen data.

> A **learning algorithm** uses pre-existing information to perform a task and is evaluated by a **performance measure**.

**The Supervised Learning Process:**
• **Task**: The problem to be solved (e.g., spam detection).
• **Information**: The labeled dataset (e.g., emails classified as 'spam' or 'not spam').
• **Performance Measure**: A metric to evaluate success (e.g., accuracy, error rate).
• **Algorithm**: The method used to infer the mapping function (e.g., Decision Tree, Linear Models).

• A **training algorithm** works by adjusting the parameters of the learning model to minimize error on the training data.

# Decision Tree Classifier

• A **Decision Tree** is a model that classifies data by asking a series of sequential, hierarchical questions.
• Each internal node represents a "test" on an attribute.
• Each branch represents the outcome of the test.
• Each leaf node represents a final **class label**.

**Decision Tree Induction** is the process of building the tree from data.
• Training algorithms generate many candidate trees and select the best one based on a performance measure.
• At each node, the data is split into distinct child nodes based on an attribute's value. Splits can be **binary** or **multi-way**.

> The **goodness of a split** is measured by how much it reduces "node impurity," or the mix of classes in the resulting nodes.

**Common Splitting Criteria:**
• **GINI Index**: Measures impurity; a split with a lower GINI index is better.
• **Information Gain & Gain Ratio**: Based on **Entropy**, which measures disorder. The split that provides the highest information gain (or gain ratio) is chosen.
• **Misclassification Error**: The proportion of incorrectly classified instances.

### Model Overfitting

• **Overfitting** occurs when a model learns the training data too well, including its noise and random fluctuations, but fails to generalize to new data.
• In decision trees, overfitting is often caused by a **high number of splits**, creating a complex tree that memorizes the data rather than learning the underlying pattern.

### Model Selection

• **Model Selection** is the process of choosing among different models or tuning parameters to find the one that generalizes best to unseen data.
• This often involves comparing models using a **validation set** not seen during training.

**Advantages of Decision Trees:**
• Easy to construct, fast to use, and highly interpretable.
• Can handle redundant or irrelevant attributes.
• Robust to noise in the data.

**Disadvantages of Decision Trees:**
• Prone to **overfitting**.
• Struggle with missing data and interacting attributes.
• Not suitable for all problem types (e.g., learning XOR relationships).

**Improving Decision Trees:**
• **Ensemble Methods**: Combine multiple models to improve performance.
• **Random Forest**: An ensemble method that builds many decision trees and classifies based on a majority vote.
• **Bagging (Bootstrap Aggregating)**: Trains multiple models on different random subsets of the training data and averages their predictions.

> [!NOTE] See Further:
> • Ensemble Methods (Boosting, e.g., AdaBoost, Gradient Boosting)
> • Cross-Validation techniques for model selection
> • Pruning methods for Decision Trees (Pre-pruning & Post-pruning)
> • Bias-Variance Tradeoff
> • Alternative Classification Algorithms (Support Vector Machines, k-Nearest Neighbors)

Induction algorithm

![[Pasted image 20251123152409.png]]
# ID3 Algorithm for Decision tree induction
**ID3** stands for **Iterative Dichotomiser 3**. It was developed by Ross Quinlan in 1986 and is one of the earliest and most influential decision tree algorithms. Its core philosophy is to build a tree in a **top-down, greedy** manner using **Information Theory**, specifically the concept of **Entropy and Information Gain**.

#### 1. Entropy
Entropy (`H(S)`) is a measure of **impurity, disorder, or uncertainty** in a dataset (`S`). In the context of classification, it tells us how "mixed" the classes are in a given node.
*   **Formula:** $H(S) = - \sum{p_i* \log{2}{p_i}}$
    *   `pᵢ` is the proportion of instances in the dataset `S` that belong to class `i`.
    *   The log is base 2 because entropy is measured in **bits**.

**Interpretation:**
*   **Entropy = 0:** The node is perfectly **pure** (all instances belong to the same class). There is no uncertainty.
*   **Entropy = 1 (maximum):** The node is perfectly **impure** (instances are evenly split between classes). Uncertainty is at its peak.

*Example:*
If a node has 10 instances: 5 "Yes" and 5 "No", the entropy is:
`H(S) = - [ (5/10)*log₂(5/10) + (5/10)*log₂(5/10) ] = - [0.5*(-1) + 0.5*(-1)] = 1`

#### 2. Information Gain (IG)
Information Gain measures the **reduction in entropy** achieved by partitioning the data based on a specific feature. It tells us how much "information" a feature gives us about the class.

*   **Formula:** $$IG(S, A) = H(S) - \sum{ \frac{|S_v|} {|S|} * H(Sᵥ) }$$
    *   `H(S)`: Entropy of the entire parent node (before the split).
    *   `A`: The feature we are testing.
    *   `Sᵥ`: The subset of data where feature `A` has value `v`.
    *   `|Sᵥ| / |S|`: The weight (proportion) of the subset `v`.

**The Rule:** The feature with the **highest Information Gain** is chosen to split the node at that step.

### The ID3 Algorithm: Step-by-Step

It's a **recursive, greedy** algorithm:
1.  **Start:** Begin at the root node with the complete dataset.
2.  **Calculate Base Entropy:** Compute the entropy of the target attribute for the current dataset.
3.  **For Each Feature:**
    *   Calculate the entropy for each subset of data created by splitting on that feature.
    *   Calculate the **weighted average** of these subset entropies.
    *   Compute the **Information Gain** for the feature: `IG = Base Entropy - Weighted Average Entropy`.
4.  **Select the Best Feature:** Choose the feature with the **highest Information Gain**.
5.  **Split the Node:** Create a new branch for each possible value of the selected feature. Partition the dataset accordingly.
6.  **Repeat Recursively:** For each new child node, repeat steps 2-5 using only the data that has reached that node.
7.  **Stopping Conditions:** The recursion stops when one of the following is true:
    *   All instances in the node belong to the **same class**. This becomes a **leaf node** labeled with that class.
    *   There are **no more features** left to split on. This becomes a **leaf node** labeled with the **majority class**.
    *   There are **no instances** in a branch. This creates a leaf node labeled with the majority class from the parent node.

--- 

Let's use the classic "Play Tennis" dataset:

| Outlook  | Temperature | Humidity | Wind   | Play Tennis? |
| :------- | :---------- | :------- | :----- | :----------- |
| Sunny    | Hot         | High     | Weak   | No           |
| Sunny    | Hot         | High     | Strong | No           |
| Overcast | Hot         | High     | Weak   | Yes          |
| Rainy    | Mild        | High     | Weak   | Yes          |
| Rainy    | Cool        | Normal   | Weak   | Yes          |
| Rainy    | Cool        | Normal   | Strong | No           |
| Overcast | Cool        | Normal   | Strong | Yes          |
| Sunny    | Mild        | High     | Weak   | No           |
| Sunny    | Cool        | Normal   | Weak   | Yes          |
| Rainy    | Mild        | Normal   | Weak   | Yes          |
| Sunny    | Mild        | Normal   | Strong | Yes          |
| Overcast | Mild        | High     | Strong | Yes          |
| Overcast | Hot         | Normal   | Weak   | Yes          |
| Rainy    | Mild        | High     | Strong | No           |

**Step 1: Root Node Entropy**
*   Total instances: 14
*   Class frequencies: [9 Yes, 5 No]
*   `H(S) = - [ (9/14)*log₂(9/14) + (5/14)*log₂(5/14) ] = 0.940`

**Step 2: Calculate IG for each feature (e.g., Outlook)**
*   Outlook has values: Sunny, Overcast, Rainy.
    *   **Sunny:** [2 Yes, 3 No] -> Entropy = 0.971
    *   **Overcast:** [4 Yes, 0 No] -> Entropy = 0
    *   **Rainy:** [3 Yes, 2 No] -> Entropy = 0.971
*   Weighted Average Entropy = (5/14)*0.971 + (4/14)*0 + (5/14)*0.971 = 0.693
*   `IG(Outlook) = 0.940 - 0.693 = 0.247`

**Step 3: Compare IGs**
*   `IG(Outlook) = 0.247`
*   `IG(Temperature) = 0.029`
*   `IG(Humidity) = 0.152`
*   `IG(Wind) = 0.048`

**Outlook has the highest IG, so it becomes the root node.**

**Step 4: Recursion**
*   The **Overcast** branch is already pure (all "Yes"), so it becomes a leaf node.
*   We now recursively run ID3 on the **Sunny** and **Rainy** branches, using only the relevant data and without the `Outlook` feature.

This process continues until the tree is fully built. The final tree might look like this:

```
        [Outlook?]
         /   |   \
        /    |    \
  Sunny/  Overcast|  \Rainy
      /           |    \
   [Humidity?]  [Yes]  [Wind?]
    /       \          /    \
High/         \Normal  /      \
  /           \      /        \
[No]         [Yes]  Strong/    \Weak
                         /      \
                       [No]    [Yes]
```

When you are at the **"Sunny" branch** of the Outlook node, you only consider the data points where `Outlook = Sunny`.

Let me show you with the actual data from our example:

**Original Dataset:**

|Outlook|Temperature|Humidity|Wind|Play Tennis?|
|---|---|---|---|---|
|Sunny|Hot|High|Weak|No|
|Sunny|Hot|High|Strong|No|
|Overcast|Hot|High|Weak|Yes|
|Rainy|Mild|High|Weak|Yes|
|Rainy|Cool|Normal|Weak|Yes|
|Rainy|Cool|Normal|Strong|No|
|Overcast|Cool|Normal|Strong|Yes|
|Sunny|Mild|High|Weak|No|
|Sunny|Cool|Normal|Weak|Yes|
|Rainy|Mild|Normal|Weak|Yes|
|Sunny|Mild|Normal|Strong|Yes|
|Overcast|Mild|High|Strong|Yes|
|Overcast|Hot|Normal|Weak|Yes|
|Rainy|Mild|High|Strong|No|

**When splitting the "Sunny" branch, you ONLY use these 5 data points:**

|Outlook|Temperature|Humidity|Wind|Play Tennis?|
|---|---|---|---|---|
|Sunny|Hot|High|Weak|No|
|Sunny|Hot|High|Strong|No|
|Sunny|Mild|High|Weak|No|
|Sunny|Cool|Normal|Weak|Yes|
|Sunny|Mild|Normal|Strong|Yes|

**And you also REMOVE the "Outlook" feature** from consideration because:

1. All these data points already have `Outlook = Sunny`
2. Splitting on Outlook again would be meaningless

So for the Sunny branch, you would calculate Information Gain using only the remaining features:
- Temperature
- Humidity
- Wind

And you would build the subtree using only those 5 "Sunny" instances.

**This is exactly why decision trees are called "recursive partitioning" algorithms** - they recursively split the data into smaller and smaller subsets, and at each step, you only work with the data that has reached that particular node in the tree.

The same logic applies to the "Rainy" branch - you would only use the data points where `Outlook = Rainy` and remove Outlook from the feature set for that branch.

| Characteristics & Advantages                               | Limitations & Disadvantages                                                                                                                |
| ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| ✅ **Designed for Classification.**                        | ❌ **No Pruning.** ID3 has no built-in pruning, making it very prone to overfitting.                                                       |
| ✅ **Uses Information Gain.** A solid theoretical foundation. | ❌ **Categorical Features Only.** It cannot handle numerical (continuous) features directly (e.g., "Age=25").                              |
| ✅ **Simple and intuitive** to understand.                  | ❌ **Sensitive to features with many levels.** Features with many unique values get artificially high IG (a problem CART avoids).          |
| ✅ **Can handle multi-class classification.**               | ❌ **Greedy.** Makes locally optimal choices without considering the global tree structure.                                                |
### Evolution: From ID3 to C4.5 and C5.0
Due to its limitations, Ross Quinlan developed successors to ID3:
*   **C4.5:** A direct improvement that can handle **numerical features**, includes **pruning** to reduce overfitting, and uses **Gain Ratio** (a normalized version of Information Gain) to avoid bias towards multi-valued features.
*   **C5.0:** A more efficient, commercial version of C4.5.



# CART Algorithm for Decision tree induction
**CART**, which stands for **Classification And Regression Trees**, is a powerful algorithm used to create decision trees. It's a foundational technique in machine learning and forms the basis for more advanced algorithms like Random Forests and Gradient Boosted Trees.

The key idea is simple: it creates a tree-like model by splitting the data into subsets based on the value of input features. The goal is to make the subsets as "pure" as possible, meaning they contain data points that are predominantly from a single class (for classification) or have very similar target values (for regression).

> CART also works for regression
#### 1. The Tree Structure
*   **Root Node:** The top node, representing the entire dataset.
*   **Internal Nodes:** Nodes that represent a decision (a split) on a feature.
*   **Leaf Nodes (or Terminal Nodes):** The final nodes that provide the prediction. No further splitting happens here.
#### 2. How it Works: The Recursive Splitting Process
The CART algorithm follows a **greedy, top-down, recursive binary splitting** approach.
*   **Greedy:** At each step, it makes the *locally optimal* split without considering future splits. It chooses the best split for that moment.
*   **Top-Down:** It starts from the root node and works its way down.
*   **Recursive:** The same splitting process is repeated for each resulting subset.
*   **Binary:** Each split creates exactly two child nodes (e.g., `Age < 30` and `Age >= 30`).
#### 3. The Stopping Criteria
The splitting process doesn't continue indefinitely. It stops when one of the following conditions is met:
*   A node becomes "pure" (e.g., all samples belong to one class).
*   The tree reaches a predefined maximum depth.
*   The number of samples in a node falls below a specified minimum threshold.
*   The improvement in purity (or error reduction) from a split is below a certain minimum.
#### Splitting Criterion: **Impurity Measures**
The algorithm searches for the feature and the threshold that **maximizes the reduction in impurity** after the split. Common impurity measures are:
1.  **Gini Impurity:** The default for CART. It measures the probability of misclassifying a randomly chosen element if it were randomly labeled according to the class distribution in the node.
    *   **Formula:** `Gini = 1 - Σ(p_i²)` where `p_i` is the probability of class `i` in the node.
    *   A Gini Impurity of 0 indicates a perfectly pure node.

**Prediction at a Leaf Node:** The class that appears most frequently (the mode) in the training samples that reach that leaf.

### The CART Algorithm: Step-by-Step
1.  **Start:** Begin at the root node with the entire dataset.
2.  **Find the Best Split:** For each feature, and for each possible threshold value of that feature, calculate the quality of the split (e.g., Gini Impurity for classification, MSE for regression).
3.  **Select the Best Split:** Choose the single feature and threshold that results in the **highest purity gain** (or lowest variance).
4.  **Split the Node:** Partition the dataset at the current node into two child nodes based on the chosen split.
5.  **Repeat Recursively:** For each new child node, repeat steps 2-4.
6.  **Stop:** Continue until one of the stopping criteria is met.
7.  **Prune the Tree (Crucial Step):** The fully grown tree is often too complex and overfits the training data. **Cost-Complexity Pruning** is used to simplify it by removing branches that have little power in predicting the target variable, resulting in a model that generalizes better to new data.

### A Simple Classification Example
Imagine we want to classify if an animal is a cat or a dog based on its **Weight** and **Height**.

| Weight (kg) | Height (cm) | Class |
| :---------- | :---------- | :---- |
| 4           | 25          | Cat   |
| 5           | 26          | Cat   |
| 20          | 50          | Dog   |
| 25          | 55          | Dog   |
| 4.5         | 24          | Cat   |
| 22          | 52          | Dog   |

1.  The CART algorithm will try all possible splits (e.g., `Weight < 10`, `Weight < 15`, `Height < 30`, etc.).
2.  It finds that the best split is **`Weight < 10`**.
    *   **Left Child (Weight < 10):** Contains 3 Cats. This node is **pure** (Gini=0).
    *   **Right Child (Weight >= 10):** Contains 3 Dogs. This node is also **pure** (Gini=0).
3.  Since both child nodes are pure, the splitting stops.

The resulting tree would look like this:
```
        [All Animals]
          /
         / Weight < 10?
        /   \
    [Yes]   [No]
    (Cats)  (Dogs)
```

| Advantages                                                                 | Disadvantages                                                                                                                              |
| -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| ✅ **Simple to understand and interpret.** The model is visually intuitive. | ❌ **Prone to Overfitting.** A deep tree will memorize the training data. Pruning is essential.                                            |
| ✅ **Can handle both numerical and categorical data.**                      | ❌ **Unstable.** Small changes in data can lead to a completely different tree.                                                            |
| ✅ **Requires little data preprocessing** (no need for scaling/dummy vars). | ❌ **Can be biased.** If one class is dominant, it can create a skewed tree.                                                               |
| ✅ **Models non-linear relationships** well.                                | ❌ **Greedy approach.** The locally optimal split may not lead to a globally optimal tree.                                                 |
