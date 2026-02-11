
**Cross-validation (CV)** is a powerful resampling technique used to assess how well a machine learning model **generalizes** to an independent dataset. It helps provide a more reliable estimate of model performance than a simple train-test split; especially when data is limited.

> [!question] Why is cross-validation needed?
> - A single train-test split can give a **noisy or biased** performance estimate (e.g., if the test set is "easy" or "hard" by chance).
> - Cross-validation **uses all available data** for both training and validation, reducing bias and variance in performance estimation.
> - It’s essential for **model selection**, **hyperparameter tuning**, and **avoiding overfitting** to a particular test set.
# k-Fold Cross-Validation
Overview:
- Split the dataset into **k** equally (or nearly equally) sized parts called **folds**.
- Train the model **k times**, each time using **k−1 folds for training** and the **remaining fold for validation**.
- Average the performance across all **k** runs to get a robust estimate.
#### Algorithm
**Input**:  
- Dataset $D = \{(x_1, y_1), (x_2, y_2), \dots, (x_n, y_n)\}$
- Number of folds \( k \) (typically 5 or 10)  
- Model \( M \) (e.g., logistic regression, random forest)  
- Evaluation metric (e.g., accuracy, RMSE)
**Output**:  
- Estimated performance $\hat{E}$ (mean ± std)

> [!info] Steps
> 1. **Shuffle** the dataset randomly (optional, but recommended—unless dealing with time series or grouped data).
> 2. **Split** \( D \) into \( k \) disjoint subsets (folds) \( $F_1, F_2, \dots, F_k$ \), each of size approximately \( $n/k$ \).
>    - For classification: use **stratified splitting** to preserve class distribution in each fold.
> 3. Initialize an empty list `scores = []`.
> 4. **For** \( i = 1 \) to \( k \):
>    - Let **validation set** = \( $F_i$ \)
>    - Let **training set** = \( $D - F_i$ \) (all data except fold \( i \))
>    - Train model \( M \) on the training set → get trained model \( $M_i$ \)
>    - Evaluate \( $M_i$ \) on validation set \( $F_i$ \) using the chosen metric → get score \( $s_i$ \)
>    - Append \( $s_i$ \) to `scores`
> 5. **Compute**:
>    - Mean score: \( $$\hat{E} = \frac{1}{k} \sum_{i=1}^{k} s_i$$ \)
>    - Standard deviation: \( $$\sigma = \sqrt{ \frac{1}{k-1} \sum_{i=1}^{k} (s_i - \hat{E})^2 }$$ \) (optional but useful)
> 6. **Return** \( $\hat{E}$ \) (and optionally $\sigma$ ) 

> [!example]
> Suppose you have 1,000 samples:
> - Each fold has 200 samples.
> - You train 5 models:
>   - Model 1: trained on folds 2–5, validated on fold 1
>   - Model 2: trained on folds 1,3–5, validated on fold 2  
>   - …  
>   - Model 5: trained on folds 1–4, validated on fold 5
> - Final score = average of 5 validation scores.
> > **Note**: The final model for deployment is usually **retrained on the full dataset** after CV is done (since CV is only for evaluation/tuning).

### Variants of k-Fold CV

| Variant                 | When to Use                             | Description                                                                           |
| ----------------------- | --------------------------------------- | ------------------------------------------------------------------------------------- |
| **Stratified k-Fold**   | Classification with imbalanced classes  | Ensures each fold has approximately the same class distribution as the full dataset.  |
| **Leave-One-Out (LOO)** | Very small datasets (n < 100)           | k = n; each sample is a validation fold once. Low bias, high variance, expensive.     |
| **Leave-P-Out**         | Small data, want exhaustive testing     | All combinations of p samples left out; computationally intense.                      |
| **Repeated k-Fold**     | Reduce randomness in fold assignment    | Run k-fold CV multiple times with different random splits; average results.           |
| **Group k-Fold**        | Data has groups (e.g., patients, users) | Ensures all samples from the same group are in the same fold → prevents data leakage. |
Possible issues of k-fold CV
### Data Leakage
- Preprocessing (e.g., scaling, imputation) must be **fitted only on the training folds** and **applied** to validation fold.
- Never compute global statistics (e.g., mean, std) using the full dataset before CV.
### Time Series Data
- Standard CV **shuffles data**, which breaks temporal order.
- Use **TimeSeriesSplit** (sklearn): trains on past, validates on future.
### Computational Cost
- k-Fold CV trains **k models** → k times slower than a single train-test split.
- For expensive models (e.g., deep nets), use **k=5** or **validation set** instead.

| Scenario                                | Recommendation                                        |
| --------------------------------------- | ----------------------------------------------------- |
| Small to medium datasets (<10k samples) | ✅ Use k=5 or k=10 CV                                  |
| Large datasets (>100k samples)          | ❌ Use simple train/val/test split (CV too slow)       |
| Model selection / hyperparameter tuning | ✅ Use CV (preferably nested CV for unbiased estimate) |
| Highly imbalanced classification        | ✅ Use **stratified k-fold**                           |
| Data with groups or repeated measures   | ✅ Use **group k-fold**                                |
> [!important]
> In **k-fold cross-validation**, the held-out fold is called the **validation set**, but **its role depends on the context**:
> - **If you're using CV for model evaluation only** → it acts like a **test set** (estimating generalization error).
> - **If you're using CV for hyperparameter tuning or model selection** → it acts like a **validation set** (to guide decisions).
