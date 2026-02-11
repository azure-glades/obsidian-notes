Task: binary classification (Yes/No, 0 - 1) for a data point X
Performance measure: probability (log probability)
Experience : Dataset of X with attributes (X1, X2 ... Xd, Y) and binary class Y (supervised)

models the probability of an event occuring or not. Assumes the prob of the event occuring to be related to a linear combination of its attributes (independent variables)

parameters of logistic regression are estimated using gradient descent or other techniques

> See further: [[Logistic Regression Example]]
## Learning Algorithm/Approach
  1. Compute a linear combination (weights): $$z = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + ... + \beta_n x_n = w^T\mathbf{x} + \beta_0$$  
  2. Apply the **logistic (sigmoid) function**: $$
    P(Y=1|\mathbf{x}) = \sigma(z) = \frac{1}{1 + e^{-z}}
    $$
    - **Log-odds (logit) form**:  $$
  \log\left(\frac{P(Y=1|\mathbf{x})}{1 - P(Y=1|\mathbf{x})}\right) = \beta_0 + \beta_1 x_1 + ... + \beta_n x_n
  $$
  3. Predict based on P > 0.5  as 1, P < 0.5 as 0
  
The log-odds of the event is a linear function of the features.

## Parameter Estimation  
- Parameters $\mathbf{\beta}$ are estimated via **Maximum Likelihood Estimation (MLE)**.  
- For $N$ samples, the likelihood is:  
  $$
  L(\mathbf{\beta}) = \prod_{i=1}^N P(Y=y_i|\mathbf{x}_i)^{y_i} \cdot (1 - P(Y=1|\mathbf{x}_i))^{1-y_i}
  $$  
- Optimization minimizes the **negative log-likelihood (log loss)**:  
  $$
  J(\mathbf{\beta}) = -\frac{1}{N}\sum_{i=1}^N \left[ y_i \log(\hat{p}_i) + (1-y_i)\log(1-\hat{p}_i) \right]
  $$  
  where $\hat{p}_i = \sigma(\mathbf{\beta}^T\mathbf{x}_i)$.  

- Common optimization methods:  
  - Gradient descent (or variants like stochastic/batch GD)  
  - Newton-Raphson / IRLS (Iteratively Reweighted Least Squares)  
  - L-BFGS (used in many libraries like scikit-learn)

## Odds Ratio
- The coefficient $\beta_j$ affects the **odds** multiplicatively, i.e how important is an attribute
  $$
  \text{Odds Ratio} = e^{\beta_j}
  $$  
  - If $\beta_j > 0$, the feature increases the odds of $Y=1$.  
  - If $\beta_j < 0$, it decreases the odds.  
- Example: If $\beta_{\text{age}} = 0.05$, then $e^{0.05} \approx 1.05$, meaning each additional year increases the odds by about 5%.

## Regularization  
To prevent overfitting, regularization adds penalty terms to the loss:  
- **L2 (Ridge)**: $\lambda \sum \beta_j^2$ → shrinks coefficients but keeps all features  
- **L1 (Lasso)**: $\lambda \sum |\beta_j|$ → can zero out coefficients (feature selection)  
- **Elastic Net**: Combines L1 and L2 penalties  


## Advantages:  
- Outputs calibrated probabilities 
- Interpretable coefficients 
- Computationally efficient  
- Low variance (stable predictions)  

## Limitations:  
- Assumes linear decision boundary in log-odds space  
- Cannot capture complex non-linear patterns
- Sensitive to outliers
- Requires sufficient data for reliable MLE  
