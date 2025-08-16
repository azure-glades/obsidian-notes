
#### Introduction to Supervised Learning
* **Goal:** Learn from past, labeled data to make future predictions.
* **Method:** Analyze past observations to draw insights and inform future decisions.
* **Key Concepts:**
    * **Discriminative features:** Features that are most useful for classifying data.
    * **Entropy and Information Gain:** Measures used to quantify a feature's discriminative power.
    * **Classification and Regression Trees (CART):** The core algorithm for building a decision tree.
    * **Random Forest:** An ensemble of decision trees used for improved performance.

>[!note] Overfitting
>Overfitting happens when a model learns the training data _too_ well. It starts to memorize the specific quirks, anomalies, and noise in the training set instead of learning the general patterns that would apply to new, unseen data. This results in increased false predictions

#### Discriminative Features: A Camera Example
* **Scenario:** A retail website like Amazon wants to predict a customer's camera rating (1-5) to improve recommendations.
* **Data:** The machine analyzes a customer's past purchases and their corresponding ratings, along with the camera's features (company, color, price, etc.).
* **Identifying Importance:** The goal is to determine which features influence a customer's rating.
* **Example Analysis:**
    * **Company:** A company (C2) received significantly more high ratings than another (C1), indicating it's a **discriminative feature**. This could be a direct preference or a proxy for other unmeasured features.
    * **Color:** Ratings were evenly distributed for black and white cameras, suggesting color is **not a discriminative feature**.
    * **Price:**
        * A price threshold of **< \$300** showed little difference in high rating probability (0.36 vs. 0.4).
        * A price threshold of **< \$500** showed a clearer difference (0.4 vs. 0.2), but the low sample size (10 examples) makes this finding weak.

>[!note] Discriminative Feature
A **discriminative feature** is a characteristic of data that is most useful for distinguishing between different classes or outcomes. In machine learning, algorithms like decision trees rely on these features to create clear decision boundaries. For example, in predicting whether a customer will give a high or low rating to a camera, the **company brand** might be a discriminative feature if cameras from one brand consistently receive high ratings, whereas **color** might not be if black and white cameras get similar ratings.

#### Quantifying Discriminativeness: Entropy and Information Gain
Entropy is a measure of the **uncertainty** or **impurity** of a dataset. 📈
* **High Entropy:** Occurs when a dataset is mixed, with a relatively even distribution of different classes. This represents high uncertainty, as you're unsure which class a new data point will belong to. For instance, a dataset with a 50/50 split of "high" and "low" ratings has maximum entropy.
* **Low Entropy:** Occurs when a dataset is "pure," with most or all of its examples belonging to a single class. This represents high certainty. An example where 90% of ratings are "high" has very low entropy.
*  **Formula:** $H(S) = -\sum_{i=1}^{k} p_i \log_2(p_i)$ where $k$ is the number of possible outcomes and $p_i$ is the probability of outcome $i$.

Entropy is crucial because it provides a quantitative way to measure how "messy" a dataset is. In decision trees, the goal is to create splits that lead to the lowest possible entropy.
##### How Splitting Reduces Entropy
When a dataset is split using a particular feature, the goal is to create subsets (or child nodes) that are **more homogeneous** than the original dataset. A good split will group most of the examples of one class into a single child node, thereby reducing the "impurity" of that node.
* The entropy of the original dataset is the starting point.
* After a split, the entropy of each new subset is calculated.
* A good split will result in child nodes with **lower entropy** compared to the original, unsplit dataset.

**Information Gain** is the measure used to quantify this reduction in entropy. It's the difference between the entropy of the original dataset and the weighted average of the entropies of the subsets created by the split.
-  **Formula:** $$\text{Information Gain}(S, A) = \text{Entropy}(S) - \sum_{v \in \text{Values}(A)} \frac{|S_v|}{|S|} \times Entropy(S_v)$$
- **Key Point:** A larger information gain means the feature is more discriminative.
- **Example:** Splitting by company provided a higher information gain than splitting by price.
**A high Information Gain** means the split on that feature was very effective at reducing uncertainty. This tells the algorithm that the feature is highly discriminative. The algorithm will choose the feature with the highest information gain to make the next split in the decision tree.
**A low Information Gain** (or zero) means the split didn't significantly reduce entropy, and the new subsets are still just as mixed as the original dataset. This indicates the feature is not very discriminative.
>Essentially, a good split maximizes Information Gain by minimizing the entropy of the resulting child nodes.

#### The Decision Tree Algorithm
The **Decision Tree Algorithm** is a supervised learning method that creates a model in the form of a tree structure. It's designed to make predictions by learning simple decision rules inferred from the data features.
* **Training Phase:** The primary goal of the training phase is to **construct the tree itself** using the provided training data. The algorithm isn't trying to make a prediction for a test case yet; it's focused on building a model that can make future predictions.
* To achieve this, the training phase performs these key steps:
	* **Learning the Structure:** The algorithm starts with a root node (representing the entire dataset) and iteratively splits it into sub-nodes. It does this by asking a question about a feature (e.g., "Is the camera company C1?").
	* **Choosing the Best Splits:** At each step, the algorithm evaluates all available features to determine which one will create the "best" split. A split is considered "best" if it results in the greatest reduction in impurity or uncertainty. It uses metrics like **Information Gain** (for classification) or **Reduction in Variance** (for regression) to quantify this.
	* **Building a Predictive Model:** The process continues until the tree's leaf nodes are relatively "pure" (meaning most of the data points in that node belong to the same class) or a stopping condition is met. The result is a tree-like flowchart that represents a set of rules learned from the data.
Steps:
    1.  Start with the full dataset.
    2.  Calculate the information gain for every available feature.
    3.  Choose the feature with the **maximum information gain** and split the data accordingly.
    4.  Repeat this process for each new subset of data, building a tree structure.
    5.  Stop splitting when no feature provides a significant information gain. The resulting nodes are **leaf nodes**.
* **Testing Phase:**
    1.  To classify a new data point, start at the root of the tree.
    2.  Follow the path down the tree by evaluating the features at each node.
    3.  The final prediction is the most frequent class label in the leaf node the data point lands in.
* **Advantages:** Easy to interpret and fast for classification.
* **Disadvantages:** Can suffer from **overfitting** (performing well on training data but poorly on new data) and is a greedy heuristic (doesn't guarantee a globally optimal tree).
* **Regression Extension:** For a real-valued target variable, use **variance** instead of entropy as the measure of disorder. Splits are chosen to maximize the reduction in variance.

#### Random Forest: An Ensemble of Decision Trees
* **Concept:** Combines multiple decision trees to improve performance and reduce overfitting. A "forest" is a collection of "trees."
* **Method:** Each tree in the forest is trained on a different, randomly selected subset of features.
* **Prediction:** For a new data point, each tree makes a prediction. The final prediction is determined by a **majority vote** among all the trees' predictions.
* **Benefit:** Considered a very powerful and successful classifier. Random forests overcomes the issue of *overfitting* which is a common problem for decision trees

Random Forest uses two main sources of randomness to ensure its trees are different:
1.  **Random Sampling of Features:** As you correctly identified, each tree is trained using a random subset of the available features. This means that a tree might focus on, say, company, price, and resolution, while another tree focuses on color, video frame rate, and customer reviews.
2.  **Random Sampling of Data:** This is the other key piece. Instead of training each tree on the entire training dataset, each tree is trained on a random sample of the training data. This process is called **bootstrap aggregation**, or **bagging**.

- A single, deep tree might **overfit** to some random noise in its training data, leading to a very confident but wrong prediction on new data.
- But when you have many such trees, all with their own unique "overfitting," those individual quirks and errors tend to **cancel each other out** when you take a majority vote.

#### Economic Applications
* **Consumer Behavior Analysis:** Predicting customer-specific preferences and ratings.
* **Market Basket Analysis:** Identifying which items are frequently purchased together to create bundles.
* **Loan Default Prediction:** Banks use a sequence of customer features to predict their likelihood of repaying a loan.
* **Fraud Transaction Analysis:** Identifying fraudulent transactions by analyzing a sequence of transaction features.
* **Public Policy Impact Assessment:** Assessing the impact of a policy by analyzing a sequence of relevant features.