| Concept          | What it means                                                                                     | Symptoms                                                                                       |
| ---------------- | ------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| **Underfitting** | The model is **too simple** to capture the underlying pattern in the data.                        | - High training **and** test error<br>- Model performs poorly even on training data            |
| **Overfitting**  | The model is **too complex** and learns the **noise** (random fluctuations) in the training data. | - Very low training error<br>- High test/validation error<br>- Fails to generalize to new data |
> **Goal**: Find the "sweet spot" where the model generalizes well to unseen data.

The ability of a model to perform well on unseen data is [[Generalization]] (how well it can generalize the distribution). Generalization 
### Bias and Variance
Bias and variance are properties of the **model’s predictions**, not the data.
#### Bias
- **Definition**: Error due to **oversimplification** — the assumptions the model makes about the data.
- **High bias** → Model ignores relevant patterns → **underfitting**.
- Example: Using a straight line to fit clearly curved data.
#### Variance
- **Definition**: Error due to **sensitivity to small fluctuations** in the training set.
- **High variance** → Model changes drastically with different training data → **overfitting**.
- Example: A high-degree polynomial that wiggles to pass through every training point.
# The Bias-Variance Decomposition
For regression (with squared error), the **expected prediction error** on new data can be decomposed as:
$$
\text{Total Error} = \text{Bias}^2 + \text{Variance} + \text{Irreducible Error}
$$
- **Bias²**: How far off the model’s predictions are from the true values **on average**.
- **Variance**: How much the predictions **fluctuate** if we train on different datasets.
- **Irreducible Error**: Noise inherent in the data (e.g., measurement errors) — **cannot be reduced** by the model.

>[!tip] Bias and variance are **inversely related**.  
> As you increase **Model Complexity** (adding more features or layers):
> 1. **Bias decreases:** The model becomes flexible enough to represent the real patterns.
> 2. **Variance increases:** The model becomes so flexible it starts chasing "ghosts" (noise) in the data.

![[Pasted image 20251222184807.png]]

| Problem        | Symptoms | Solutions |
|----------------|--------|---------|
| **Underfitting** (High Bias) | High train/test error | - Use a more complex model<br>- Add more relevant features<br>- Reduce regularization<br>- Train longer (for deep learning) |
| **Overfitting** (High Variance) | Low train error, high test error | - Get more training data<br>- Use simpler model<br>- Apply regularization (L1/L2, dropout)<br>- Use cross-validation<br>- Early stopping<br>- Feature selection |
Think of **bias** as **being consistently wrong in the same way** (e.g., always aiming 5 cm left of a target), while **variance** is **being inconsistent** (shots scattered widely, even if centered).
- **High bias** = all shots clustered far from bullseye.  
- **High variance** = shots spread all over, even if average is near center.  
- **Ideal** = tight cluster **on** the bullseye (low bias + low variance).

|                | Underfitting        | Overfitting         |
|----------------|---------------------|---------------------|
| **Cause**      | Model too simple    | Model too complex   |
| **Bias**       | High                | Low                 |
| **Variance**   | Low                 | High                |
| **Generalization** | Poor             | Poor                |
