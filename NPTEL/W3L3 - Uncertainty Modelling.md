### Uncertainty Modeling in AI for Economics

#### 1. Sources of Uncertainty in Predictions
* **Aleatoric Uncertainty:** Arises from imprecise or noisy observations and missing data.
* **Epistemic Uncertainty:** Arises from limitations in the model itself (e.g., using a linear model for a non-linear relationship).
* **Significance:** Acknowledging and quantifying uncertainty is crucial because predictions are rarely perfectly accurate. This requires using probability theory to provide not just a single number, but a range of possible outcomes.

---

#### 2. Key Concepts in Probability Theory
* **Random Experiment:** "A process that can have several possible outcomes, but we cannot say that for one particular run of the experiment which outcome will happen."
* **Sample Space:** "The set of all possible outcomes of a random experiment."
* **Random Variable (X):** "A mapping from the event space (subsets of the sample space) to the space of real numbers."
* **Support:** "The set of unique values that a random variable can take."
* **Random Variable Types:**
    * **Discrete Random Variable (DRV):** Has a discrete support set (e.g., Bernoulli, Binomial, Poisson).
    * **Continuous Random Variable (CRV):** Has a continuous support set (e.g., Uniform, Gaussian, Gamma).
* **Probability Mass Function (PMF):** For a DRV, it's the probability that the random variable takes on a specific value.
* **Probability Density Function (PDF):** For a CRV, it's a function that describes the relative likelihood for a random variable to take on a given value.
* **Cumulative Distribution Function (CDF):** Defines the probability that a random variable will take a value less than or equal to a specific number.

---

#### 3. Joint and Conditional Probability
* **Joint Distribution:** "The probability distribution for two or more random variables that can occur simultaneously."
* **Independence:** Two random variables, $X$ and $Y$, are independent if their joint distribution can be factored into the product of their individual distributions: $f(x, y) = f(x) f(y)$.
* **Conditional Distribution:** "The probability of one event happening, given that another event has already occurred."
    * The conditional distribution of $Y$ given $X$ is defined as $f(y|x) = f(x, y) / f(x)$.

---

#### 4. Bayesian Networks
* **Purpose:** To model complex systems with many uncertain, interdependent variables in an efficient way.
* **Structure:** A directed graph where each vertex represents a random variable. The edges represent conditional dependencies.
* **Conditional Probability Tables (CPTs):** A conditional distribution is defined at each node based on its parent nodes.
* **Factorization:** The joint distribution of all variables in the network can be expressed as the product of the conditional distributions of each variable given its parents.
* **Probabilistic Inference:** Using known values of some variables, a Bayesian network can be used to predict the possible values of other variables through a process of calculation.

---

#### 5. Characterizing Distributions from Data
* **Approximation:** Real-world data may not follow a perfect distribution, but it can be approximated by known parametric distributions (e.g., Gaussian for real numbers, Bernoulli for binary outcomes).
* **Histogram:** By observing the histogram of data, we can identify which standard PMF or PDF it most closely resembles.
* **Maximum Likelihood Estimate (MLE):** A method used to estimate the unknown parameters of a chosen distribution (e.g., mean and variance for a Gaussian distribution). It works by finding the parameter values that maximize the probability of observing the given data.

---

#### 6. Expectation and Variance
* **Expectation (E[X]):** "The probability-weighted average value of a random variable." It represents the average case scenario.
* **Variance (Var[X]):** A measure of how much a random variable's values are likely to deviate from its expected value. It quantifies the spread of the distribution.

---

#### 7. Applications in Economics
* **Financial Risk Assessment:** Bayesian networks model complex dependencies between economic variables to assess risk more accurately.
* **Market Analysis:** They can represent market dynamics by modeling relationships between supply, demand, prices, and consumer behavior.
* **Expectation-Based Risk Analysis:** Expectations and variance are used in decision-making under uncertainty, such as in betting or stock market predictions, to understand average outcomes and potential risks.
* **Variable Selection:** Bayesian networks can help identify key economic variables that influence a prediction.