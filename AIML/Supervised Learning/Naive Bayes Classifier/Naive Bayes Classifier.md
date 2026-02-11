> Uses bayes theorem to calculate probability of a data point belonging to a class

**Task:** For a given data point $(x_1, x_2, x_3, \dots, x_d)$ predict the class $Y$

**Experience (Dataset):** Set of data points with attributes $(X_1, X_2, X_3 \dots X_d, Y)$

**Performance Measure:** Depends (it's probability or log probability)

## Learning Algorithm/Approach
1.  **Compute Posterior Probability:** Calculate $P(Y | x_1, x_2, x_3 \dots x_d)$, the probability of data point $X$ being class $Y$.
    *   Formula: $$P(Y | X) = \frac{P(X | Y) \times P(Y)}{P(X)}$$
2.  **Maximum Posterior:** Find the class $Y$ which has the highest $P(Y|X)$.
Alternatively, one can also use log probability instead

### Terminology
*   **$P(Y)$**: Called the **prior**
*   **$P( X | Y)$**: Called the **likelihood**, i.e., the probability of getting $X = (x_1, x_2, x_3 \dots x_d)$ given class $Y$.

## The Naive Bayes Assumption

$$P(x_1, x_2, x_3 \dots x_d | Y ) = P(x_1 | Y) \times P(x_2|Y) \dots \times P(x_d | Y)$$

*   This holds when all attributes are independent (which is often not true).
*   However, this holds true in most practical cases, even when attributes are not fully independent.
*   $Y$ can be a nominal, binary, or ordinal variable etc.

## Handling Attribute Types

### If $X_i$ is Discrete
*   $P(x_i | Y)$ can be calculated easily:$$P(x_i | Y) = \frac{\text{no of times we have } X_i = c}{\text{no of data points } n}$$

### If $X_i$ is Continuous
*   **Distribution Approach:** Assume $X_i$ follows a distribution (like Gaussian) and calculate sample mean, sample variance, etc.
*   **Binning Approach:** Put $X_i$ into classes/bins so it becomes a categorical variable.

## Handling Zero Probability (Estimation)
**Key Issue:** If the number of times we have $X_i = c$ is 0, then $P(x_i | Y)$ is 0.
**Resolution:** Use estimation methods to resolve this problem.
*   **Laplace Estimate:**$$\frac{n_c + 1}{n + v}$$
    Where $v$ is the number of variables.
*   **m-estimate:**$$P(X_i = c | Y) = \frac{n_c + mp}{n+m}$$
    Where $m$ is a hyperparameter and $p$ is the priori.

## Advantages
*   Not affected by outliers as much
*   Handles missing values by ignoring that attribute when calculating probability
*   Not affected by irrelevant attributes

## Problems
*   Naive Bayes condition is not always true.
*   High correlation attributes and redundant attributes make it fail.

> See further: [[Bayesian Belief Networks]]

> See example : [[Naive Bayes Discreet Variable Example]], [[Naive Bayes Continuous Variable Example]]