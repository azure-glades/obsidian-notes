## Feature Scaling
Without preprocessing, the variable with the largest range will dominate the distance calculation.
### 1. Standardization (Z-Score)
Transforms data so it has a mean of 0 and a standard deviation of 1.$$z = \frac{x - \mu}{\sigma}$$
- **Use case:** Best when the data follows a normal distribution or when you have outliers.
### 2. Normalization (Min-Max Scaling)
Squashes the data into a fixed range, usually `[0, 1]`. $$x_{new} = \frac{x - x_{min}}{x_{max} - x_{min}}$$
- **Use case:** Best when you know the boundaries of your data and want to ensure all features have the exact same weight.

## Handling Missing Data
Clustering algorithms usually cannot handle "NaN" or empty cells. You have three main strategies:
1. **Deletion:** Remove any object (row) with missing values.
    - _Risk:_ You might lose too much valuable data.
2. **Imputation:** Fill in the blanks.
    - **Mean/Median Imputation:** Fill with the average of that column.
    - **K-NN Imputation:** Find the "K" most similar objects and fill the gap based on their values (very effective for clustering).
3. **Proximity Adjustment:** Modify the distance formula. If two objects are being compared and one has a missing value for attribute $i$, simply calculate the distance using the remaining $p-1$ attributes and scale the result up.
