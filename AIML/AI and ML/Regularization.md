
**Regularization** is a technique used to prevent **overfitting** by discouraging a model from becoming overly complex.

Think of it as a "simplicity tax." When a model is too flexible, it starts memorizing the noise and random fluctuations in your training data rather than learning the actual underlying patterns. Regularization adds a penalty to the model for having large or complex weights, forcing it to stay "simple" and generalize better to new, unseen data.

Normally, a model tries to minimize a **Loss Function** (the error between predictions and reality). Regularization modifies this by adding a **Penalty Term**:
$$\text{Total Cost} = \text{Loss Function} + \lambda(\text{Penalty})$$
- **$\lambda$ (Lambda):** This is a tuning parameter that controls how much you want to penalize complexity.
    - If $\lambda = 0$, there is no regularization.
    - If $\lambda$ is very high, the model becomes extremely simple (potentially underfitting).
### L1 Regularization (Lasso)
L1 adds the **absolute value** of the weights as a penalty.
- **Key Feature:** It can force some weights to become exactly **zero**.
- **Best For:** Feature selection.
	- It effectively "turns off" unimportant features, leaving you with a sparse, interpretable model.
- **Formula:** $$\lambda \sum_{i=1}^n |w_i|$$
### L2 Regularization (Ridge)
L2 adds the **squared value** of the weights as a penalty.
- **Key Feature:** It shrinks all weights towards zero but rarely makes them exactly zero.
- **Best For:** Dealing with multicollinearity (highly correlated features) and preventing any single feature from having a dominant influence.
- **Formula:** $$\lambda \sum_{i=1}^n w_i^2$$
### Elastic Net
This is a hybrid approach that combines both L1 and L2 penalties. It’s useful when you have multiple features that are correlated with each other.

Advantage:
- **Reduces Variance:** It stops the model from being too sensitive to small changes in the training data.
- **Improves Generalization:** A regularized model usually performs much better on the test set even if its performance on the training set drops slightly.
- **Handles High Dimensionality:** It allows you to train models even when you have more features than data points.
