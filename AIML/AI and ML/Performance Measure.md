
In machine learning, **performance** is a quantitative measure of how well a model achieves its specific task (e.g., how often it's right, or how close its guesses are to the truth). These are some performance measures for classification
### 1. Confusion Matrix
The confusion matrix is the foundation for most classification metrics. For binary classification, it’s a 2×2 table:

|                        | **Actual Positive** | **Actual Negative** |
| ---------------------- | ------------------- | ------------------- |
| **Predicted Positive** | True Positive (TP)  | False Positive (FP) |
| **Predicted Negative** | False Negative (FN) | True Negative (TN)  |
- **TP**: Correctly predicted positive
- **FP**: Incorrectly predicted positive (Type I error)
- **FN**: Incorrectly predicted negative (Type II error)
- **TN**: Correctly predicted negative
### 2. Accuracy
**Definition**: Proportion of correct predictions (both positive and negative) among all predictions.
$$
\text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN}
$$
> **Limitation**: Can be misleading for imbalanced datasets (e.g., 99% negative class → high accuracy even if model ignores positives).

### 3. Precision
**Definition**: Proportion of predicted positives that are actually positive. Answers: “Of all instances I labeled positive, how many were correct?”
$$
\text{Precision} = \frac{TP}{TP + FP}
$$
> High precision → Few false positives  
> Useful when cost of false positives is high (e.g., spam detection: don’t want to mark real emails as spam)
### 4. Recall (Sensitivity or True Positive Rate)
**Definition**: Proportion of actual positives correctly identified. Answers: “Of all actual positives, how many did I catch?”
$$
\text{Recall} = \frac{TP}{TP + FN}
$$
> High recall → Few false negatives  
> Critical when missing a positive is costly (e.g., disease diagnosis: don’t want to miss infected patients)
### 5. Specificity (True Negative Rate)
**Definition**: Proportion of actual negatives correctly identified.
$$
\text{Specificity} = \frac{TN}{TN + FP}
$$
> Complement of false positive rate:  
> $\text{FPR} = 1 - \text{Specificity} = \frac{FP}{TN + FP}$
### 6. F1 Score
**Definition**: Harmonic mean of precision and recall. Balances the two, especially useful when class distribution is uneven.
$$
\text{F1} = 2 \cdot \frac{\text{Precision} \cdot \text{Recall}}{\text{Precision} + \text{Recall}}
$$
> Ranges from 0 to 1; higher is better.  
> Preferred over accuracy in imbalanced scenarios.
> **Why harmonic mean?** Arithmetic mean would overestimate performance if one of precision/recall is very low.
### 7. Fβ Score (Generalized F-Measure)
Adjusts the balance between precision and recall using a parameter β:
$$
F_\beta = (1 + \beta^2) \cdot \frac{\text{Precision} \cdot \text{Recall}}{(\beta^2 \cdot \text{Precision}) + \text{Recall}}
$$
- β = 1 → F1 (equal weight)
- β > 1 → Recall favored (e.g., β = 2)
- β < 1 → Precision favored (e.g., β = 0.5)
### 8. ROC Curve & AUC
- **ROC (Receiver Operating Characteristic)**: Plots **True Positive Rate (Recall)** vs. **False Positive Rate (1 − Specificity)** at various threshold settings.
- **AUC (Area Under Curve)**: Summarizes ROC performance; AUC = 1 → perfect classifier, AUC = 0.5 → random guessing.
> Useful for comparing models independent of classification threshold.
#### When to Use Which Metric?

| Scenario                               | Preferred Metric      |
| -------------------------------------- | --------------------- |
| Balanced classes, general purpose      | Accuracy              |
| Imbalanced classes                     | F1, Precision, Recall |
| Avoid false positives                  | Precision             |
| Avoid false negatives                  | Recall                |
| Need threshold-independent view        | AUC-ROC               |
| Medical diagnosis (catch all diseases) | High Recall           |
| Fraud detection (avoid false alarms)   | High Precision        |
>[!example]
> Suppose:
> - TP = 80, FP = 20, FN = 10, TN = 90
> 
> Then:
> - Accuracy = (80 + 90) / (80+20+10+90) = 170/200 = **0.85**
> - Precision = 80 / (80 + 20) = **0.80**
> - Recall = 80 / (80 + 10) = **0.89**
> - F1 = 2 × (0.80 × 0.89) / (0.80 + 0.89) ≈ **0.84**

## Error Based metrics
Generally for regression models:
### 1. Mean Absolute Error (MAE)  
Measures the **average magnitude of errors** (ignoring direction — i.e., sign).
$$
\text{MAE} = \frac{1}{n} \sum_{i=1}^{n} |y_i - \hat{y}_i|
$$
- **Pros**: Easy to interpret (same units as target); robust to outliers.  
- **Cons**: Doesn’t penalize large errors heavily.  
- **Use when**: You want to understand average prediction error in real-world units.
### 2. Mean Squared Error (MSE)  
Measures the **average of squared errors**.
$$
\text{ MSE } = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2
$$
- **Pros**: Differentiable; penalizes large errors more (due to squaring).  
- **Cons**: Sensitive to outliers; units are squared (harder to interpret).  
- **Use when**: Optimizing during training (e.g., least squares) or when large errors are especially undesirable.
### 3. Root Mean Squared Error (RMSE)  
Square root of MSE — brings the error back to the **original units** of the target.
$$
\text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2}
$$
- **Pros**: Interpretable (same units as target); emphasizes larger errors.  
- **Cons**: Still sensitive to outliers.  
- **Most widely used** in practice for regression.
> **RMSE ≥ MAE**, and the gap increases when predictions have large errors.
### 4. Mean Absolute Percentage Error (MAPE)  
Measures **average percentage error** — useful for relative error assessment.
$$
\text{MAPE} = \frac{100\%}{n} \sum_{i=1}^{n} \left| \frac{y_i - \hat{y}_i}{y_i} \right|
$$
- **Pros**: Unit-free; easy to explain (e.g., “average error is 5%”).  
- **Cons**:  
  - **Undefined when \(y_i = 0\)**  
  - Biased toward underestimates (asymmetric)  
  - Can explode if actual values are very small
> Often used in business/forecasting (e.g., sales, demand prediction).