Prevents overfitting, decreases generalization error

A fully grown decision tree tends to:
- Fit the training data **too closely**, including noise or outliers.
- Have **high variance**: small changes in training data lead to very different trees.
- Perform **poorly on test/validation data**, even if it achieves near-perfect accuracy on training data.
Pruning removes sections of the tree that provide little predictive power

### 1. Pre-Pruning (Early Stopping)
Stop the tree from growing **before** it perfectly classifies the training set.
**Common stopping criteria:**
- Maximum depth (`max_depth`)
- Minimum number of samples required to split a node (`min_samples_split`)
- Minimum number of samples required in a leaf (`min_samples_leaf`)
- Minimum improvement in impurity required to split (`min_impurity_decrease`)

**Pros**: Faster training; less risk of overfitting.  
**Cons**: **"Horizon effect"** - may stop too early and miss important patterns that would appear deeper in the tree.
### 2. Post-Pruning (Cost-Complexity Pruning)
- **First**, grow the tree to its full depth (until leaves are pure or meet some minimal stopping rule).
- **Then**, prune it back by **removing branches** that do not contribute meaningfully to predictive accuracy.
**Pros**: More accurate than pre-pruning in practice; avoids the horizon effect.  
**Cons**: More computationally expensive (must grow full tree first).

| Strategy         | When Applied  | Key Advantage                 | Key Risk                     |
| ---------------- | ------------- | ----------------------------- | ---------------------------- |
| **Pre-pruning**  | During growth | Fast, simple                  | May underfit (stop too soon) |
| **Post-pruning** | After growth  | Better generalization, robust | Slower, more memory use      |
