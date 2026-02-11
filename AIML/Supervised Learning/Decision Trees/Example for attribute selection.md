To select the best attribute, a decision tree must quantify "purity." We want to split a group of data so that the resulting branches are as "single-class" as possible.

## 2. Visualizing Impurity Changes

Impurity is a function of class distribution. If you have two classes (A and B), the measures change as the probability $p$ of Class A moves from $0$ to $1$.
- **At $p=0.5$ (50/50 mix):** All measures are at their **maximum**. This is the highest "disorder."
- **At $p=0$ or $1$ (Pure):** All measures are **0**. There is no uncertainty.
- **The Shape:** Entropy is a steep curve (peaking at $1.0$), while Gini is flatter (peaking at $0.5$). Misclassification error is a simple triangle.

## 3. When to Use Which?

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

---

**Summary Table**

| **Task**                    | **Metric** | **Key Advantage**                     |
| --------------------------- | ---------- | ------------------------------------- |
| **Fast Classification**     | Gini       | Computational speed (no logs).        |
| **Balanced Classification** | Entropy    | High sensitivity to impurity changes. |
| **Many-valued Features**    | Gain Ratio | Prevents overfitting to unique IDs.   |
| **Predicting Numbers**      | Variance   | Minimizes the distance from the mean. |
