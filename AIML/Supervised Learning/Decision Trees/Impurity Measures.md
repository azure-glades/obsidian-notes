In a decision tree, the goal is to split the data into groups that are as **homogeneous** (pure) as possible. Attribute selection is the process of deciding which feature—and at what specific value—will create the "best" split.
To determine the "best" split, algorithms use **Impurity Measures**. These measures quantify how mixed the classes are in a particular node.

These are the core metrics used to evaluate the quality of a single node.
### Misclassification Error
This is the simplest measure. It calculates the proportion of samples that do not belong to the most frequent class in a node.
$$\text{Error} = 1 - \max(p_i)$$

- **Pros:** Very intuitive.
- **Cons:** Not sensitive enough for growing trees. It often fails to capture improvements in "purity" that don't immediately change the majority class, which is why it's rarely used for splitting.
### Entropy
Borrowed from Information Theory, entropy measures the amount of "disorder" or uncertainty in a dataset.
$$\text{Entropy}(S) = -\sum_{i=1}^{c} p_i \log_2(p_i)$$
- **Range:** $0$ (completely pure) to $1$ (equally split between two classes).
- **Characteristic:** It is more computationally expensive than Gini due to the log function but provides a very strong "penalty" for impurity.

For a node (or dataset) $S$, $p_i$ is simply the count of samples belonging to class $i$ divided by the total number of samples in that node.
$$p_i = \frac{\text{Number of samples in class } i}{\text{Total number of samples in node } S}$$
> [!example]
> Imagine a node with 10 samples: 7 are "Yes" and 3 are "No".
> - **$p_{Yes}$** $= 7/10 = 0.7$
> - **$p_{No}$** $= 3/10 = 0.3$
> The entropy for this node would be:
> $$\text{Entropy}(S) = -(0.7 \cdot \log_2(0.7) + 0.3 \cdot \log_2(0.3)) \approx 0.88$$
> 

### Gini Index (Gini Impurity)
Used by the CART algorithm, it measures the probability of a random element being incorrectly classified if it were labeled according to the distribution in the node.
$$\text{Gini} = 1 - \sum_{i=1}^{c} (p_i)^2$$
- **Range:** $0$ to $0.5$ (for binary classification).    
- **Pros:** Computationally faster than entropy (no logarithms). It is the default in many libraries like Scikit-Learn.

![[Pasted image 20260131104021.png]]

# Selection Criteria
These formulas use the impurity measures above to compare different attributes.
### Information Gain
This is the decrease in entropy after a dataset is split on an attribute.
$$\text{Gain}(S, A) = \text{Entropy}(S) - \sum_{v \in Values(A)} \frac{|S_v|}{|S|} \text{Entropy}(S_v)$$
The algorithm calculates the Information Gain for every attribute and chooses the one with the highest value.
### Gain Ratio
A major flaw of Information Gain is its bias toward attributes with many levels (e.g., a "Customer ID" column would have perfect Information Gain but be useless for prediction). Gain Ratio corrects this by normalizing the gain using "Split Information."
$$\text{Gain Ratio} = \frac{\text{Information Gain}}{\text{Split Info}}$$
- **Split Info:** Measures the entropy of the attribute itself (how "spread out" the attribute values are). If an attribute has too many unique values, the denominator becomes large, lowering the overall Gain Ratio. $$\text{SplitInfo}_A(S) = -\sum_{j=1}^{k} \frac{|S_j|}{|S|} \log_2 \left( \frac{|S_j|}{|S|} \right)$$
> [!example]
> Suppose you are splitting on an attribute "Outlook" which has 3 possible values: **Sunny (5 samples)**, **Overcast (4 samples)**, and **Rainy (5 samples)**. Total samples $|S| = 14$.
> 1. Calculate the proportions for each branch:
>     - $5/14, 4/14, 5/14$
> 2. Plug them into the formula: $$\text{SplitInfo} = -\left( \frac{5}{14}\log_2\frac{5}{14} + \frac{4}{14}\log_2\frac{4}{14} + \frac{5}{14}\log_2\frac{5}{14} \right) \approx 1.577$$

| **Parameter**         | **Used In** | **Characteristics**                                                      |
| --------------------- | ----------- | ------------------------------------------------------------------------ |
| **Gini Index**        | CART        | Efficient; favors larger partitions; easy to compute.                    |
| **Information Gain**  | ID3         | Uses Entropy; biased toward attributes with many categories.             |
| **Gain Ratio**        | C4.5        | Normalizes Information Gain; handles high-cardinality attributes better. |
| **Misclassification** | (Rarely)    | Simplest but lacks the sensitivity needed for tree induction.            |

> [!question]
> Imagine a small dataset where we want to predict if someone will **Play Golf** based on the **Wind** condition.
> **Dataset:** 10 Days
> - **Total Play:** 6 "Yes", 4 "No"
> - **Attribute (Wind):**
>     - **Weak Wind (6 days):** 5 "Yes", 1 "No"
>     - **Strong Wind (4 days):** 1 "Yes", 3 "No"
> 

> [!example]- Steps
> ### Step A: Calculate Parent Impurity (Entropy)
> Before splitting, we calculate the disorder of the whole group.
> $$Entropy(S) = -(\frac{6}{10}\log_2\frac{6}{10} + \frac{4}{10}\log_2\frac{4}{10}) \approx 0.97$$
> ### Step B: Calculate Child Impurity (After Split)
> We calculate entropy for each branch of "Wind":
> - **Weak Wind:** $-(5/6\log_2 5/6 + 1/6\log_2 1/6) \approx 0.65$
> - **Strong Wind:** $-(1/4\log_2 1/4 + 3/4\log_2 3/4) \approx 0.81$
> **Weighted Average Entropy:** $(\frac{6}{10} \times 0.65) + (\frac{4}{10} \times 0.81) = 0.714$
> ### Step C: Final Selection Measures
> 1. **Information Gain:** $0.97 - 0.714 = \mathbf{0.256}$
> 2. Split Info (for Gain Ratio): Calculate entropy of the Wind attribute itself (proportions 6/10 and 4/10).$$\text{SplitInfo} = -(\frac{6}{10}\log_2\frac{6}{10} + \frac{4}{10}\log_2\frac{4}{10}) = 0.97$$3. **Gain Ratio:** $\text{Info Gain} / \text{Split Info} = 0.256 / 0.97 = \mathbf{0.263}$    

# When to use
### Classification: Gini vs. Entropy
For standard classification, both usually produce very similar trees.
- **Gini Index:** The default for **CART** (Scikit-Learn). It is computationally faster because it doesn't use logarithms—just simple squares. It tends to isolate the largest class into its own branch.
- **Entropy:** Used in **ID3/C4.5**. It is more "aggressive" at penalizing impurity. Use this if you want a more balanced tree or if you are specifically interested in Information Theory.
### The "High Cardinality" Problem: Gain Ratio
If an attribute has too many unique values (e.g., "Student_ID" or "Date"), **Information Gain** will falsely rank it as the best split because every leaf becomes "pure" by accident.
- **Use Gain Ratio** to normalize this. It divides the gain by the "intrinsic information" of the attribute, penalizing attributes that split the data into too many tiny pieces.
### Regression Trees: Variance Reduction
In regression, we aren't predicting "Yes/No" but a **number** (e.g., House Price). We don't use Gini or Entropy here.
- **Measure:** **Mean Squared Error (MSE)** or **Variance**.
- **Logic:** The algorithm tries to find a split that results in the lowest variance within the child nodes. It wants the numbers in each branch to be as close to their average as possible.