K-Nearest Neighbors (KNN) is a simple, instance-based (or lazy) learning algorithm used for both classification and regression. The core idea is intuitive:
> **“Things that are similar tend to belong to the same class (or have similar values).”**

### Key Characteristics:
- **Instance-based / Lazy Learning**:  
  No explicit model is built during training. All computation happens at prediction time.
- **Non-parametric**:  
  Makes no assumptions about the underlying data distribution.
- **Sensitive to Distance Scale**:  
  Features with larger scales can dominate distance calculations—so feature scaling (e.g., normalization) is often important.
- **Choice of K**:  
  - Small K (e.g., K=1): model is sensitive to noise but captures fine details (low bias, high variance).
  - Large K: smoother decision boundaries, more robust to noise but may oversimplify (high bias, low variance).

> [!tldr] Steps
> 1. **Store the Training Data**:  
>    Unlike many algorithms that "learn" a model during training, KNN simply memorizes all training examples (feature vectors and their labels).
> 2. **When Predicting for a New Instance**:  
>    - Compute the distance (e.g., Euclidean, Manhattan) between the new instance and **all** training instances.
>    - Identify the **K nearest neighbors**—the K training points with the smallest distances.
>    - For **classification**: assign the class that is most common among those K neighbors (majority vote).
>    - For **regression**: predict the average (or weighted average) of the target values of the K neighbors.

> [!important] Tie Breaking
> In some edge cases there is a **tie in the voting** among the k nearest neighbors (e.g., 2 neighbors of class A and 2 of class B when k = 4). This is seen in binary classification when k is even.
> There are many ways to break ties:
> - Use an odd value of k (avoids this edge case completely in binary classification)
> - Break ties by distance (weighted voting). Closer points have more importance than farther points. Ex: $$\text{Weight of neighbhour i} = \frac{1}{d_i}$$
> - Randomly pick a class
> - Pick the class of the closest point
> - Reduce k by 1 and see the majority class
> 

> [!example]
> Suppose you have a 2D dataset with points labeled as "red" or "blue."  
> To classify a new point:
> - Find its 5 nearest neighbors.
> - If 4 are red and 1 is blue → predict "red."

# Distance Metrics
The choice of distance metric directly impacts model performance, since it controls what the nearest neighbhors are

### Manhattan Distance (L1 Norm)
**Formula**:  
$$
d(\mathbf{x}, \mathbf{y}) = \sum_{i=1}^n |x_i - y_i|
$$

- **Interpretation**: Distance when you can only move along axes (like city blocks in Manhattan).
- **Best for**: 
  - Grid-like paths or when outliers are present (less sensitive to large deviations than Euclidean).
  - Also works well with high-dimensional sparse data (e.g., in some NLP tasks).
- **Advantage**: More robust to noise in some contexts because it doesn’t square differences.

### Euclidean Distance (L2 Norm)
**Formula**:  
$$
d(\mathbf{x}, \mathbf{y}) = \sqrt{\sum_{i=1}^n (x_i - y_i)^2}
$$
- **Interpretation**: Straight-line ("as-the-crow-flies") distance between two points in Euclidean space.
- **Best for**: Continuous numerical features with similar scales (e.g., height, weight, temperature).
- **Caveats**: 
  - Sensitive to feature scale—always standardize (e.g., z-score) or normalize features first.
  - Performance degrades in very high dimensions (“curse of dimensionality”).
### Minkowski Distance (Generalized Lp Norm)
**Formula**:  
$$
d(\mathbf{x}, \mathbf{y}) = \left( \sum_{i=1}^n |x_i - y_i|^p \right)^{1/p}
$$

- When \( p = 1 \) → Manhattan  
- When \( p = 2 \) → Euclidean  
- **Best for**: When you want to tune the behavior of the distance metric via parameter \( p \).
- **Use case**: Rarely tuned in practice, but useful theoretically to unify distance concepts.
### Cosine Similarity (Not a true distance, but often used)
**Formula**:  
$$
\text{similarity} = \frac{\mathbf{x} \cdot \mathbf{y}}{\|\mathbf{x}\| \|\mathbf{y}\|} \quad \Rightarrow \quad \text{Cosine Distance} = 1 - \text{similarity}
$$

- **Interpretation**: Measures the angle between vectors, ignoring magnitude.
- **Best for**: 
  - Text data (TF-IDF vectors), recommendation systems, or any case where direction matters more than size.
  - Example: Two documents may have very different lengths but similar word proportions - cosine treats them as close.
- **Note**: Not suitable when magnitude carries important information (e.g., income vs. age).

### Hamming Distance
**Formula**:  
$$
d(\mathbf{x}, \mathbf{y}) = \frac{1}{n} \sum_{i=1}^n \mathbb{1}(x_i \ne y_i)
$$

- **Interpretation**: Count of how many changes are needed to transmute x to y (proportion of differences)
- **Best for**: 
  - Categorical or binary data (e.g., DNA sequences, one-hot encoded features).
  - Comparing strings of equal length.
- **Limitation**: Doesn’t work well with continuous or ordinal data.

| Data Type                    | Recommended Metric(s)                                            |
| ---------------------------- | ---------------------------------------------------------------- |
| Continuous, scaled features  | Euclidean or Manhattan                                           |
| High-dimensional sparse data | Manhattan or Cosine                                              |
| Text / document vectors      | Cosine similarity                                                |
| Categorical / binary         | Hamming or Jaccard (for sets)                                    |
| Mixed data types             | Consider **Gower distance** (not standard in sklearn but useful) |

# Scaling
kNN is very sensitive to the scale of data.
KNN relies on **distance calculations** (e.g., Euclidean, Manhattan) between data points. If features are on vastly different scales, the feature with the **largest magnitude will dominate the distance**, effectively drowning out the influence of smaller-scale features.

Suppose you have:
- `Age` (range: 18–80)
- `Income` (range: \$30,000–\$150,000)

Without scaling, a difference of \$1,000 in income will appear **much larger** than a 10-year difference in age—even if age is more meaningful for your prediction task. The distance will be **biased toward income**, leading to poor or misleading neighbor selection.

> **KNN is not scale-invariant** — unlike decision trees or random forests, it *does not* automatically handle features with different units or ranges.

| **Technique**                       | **Method**                                                               | **When to Use**                                                               |
| ----------------------------------- | ------------------------------------------------------------------------ | ----------------------------------------------------------------------------- |
| **Standardization** (Z-score)       | Rescales data so it has a **mean of 0** and **standard deviation of 1**. | Best when your data follows a Gaussian (normal) distribution or has outliers. |
| **Normalization** (Min-Max Scaling) | Rescales data to a fixed range, usually **[0, 1]**.                      | Best when you don't have many outliers and want a bounded range.              |
| **Robust Scaling**                  | Uses median and interquartile range.                                     | Best if your dataset has **significant outliers** that would skew the mean.   |
## Standardization
$$
x' = \frac{x - \mu}{\sigma}
$$
- Centers data to mean = 0, scales to standard deviation = 1.
- **Best when**: Features are roughly normally distributed or you don’t know the distribution.
- **Robust to outliers?** No (mean and std are sensitive to extremes)
> Use `StandardScaler` in scikit-learn.
## Normalization
$$
x' = \frac{x - x_{\min}}{x_{\max} - x_{\min}}
$$
- Scales all features to a fixed range (typically [0, 1]).
- **Best when**: You know the approximate upper/lower bounds and data isn’t heavily skewed.
- **Robust to outliers?** No. Outliers stretch the range.
> Use `MinMaxScaler` in scikit-learn.

> **Never fit the scaler on the full dataset before splitting!**  
> Always fit the scaler **only on training data**, then transform both training and test sets.
### When is scaling not needed?
- All features are already in the **same unit and scale** (e.g., all pixel intensities from 0–255).
- You’re using a **non-distance-based similarity** like cosine (but even then, scaling may help depending on context).