

**Scenario:** We want to predict if a student will **Pass** (1) or **Fail** (0) an exam based on the number of hours they studied ($X$).

### 1. The Dataset
Let's assume we have trained our model and found the optimal parameters (weights) using gradient descent.

*   **Input ($X$):** Hours studied
*   **Parameters:**
    *   **Weight ($w$):** 1.5
    *   **Bias ($b$):** -4

### 2. The Prediction Task
Predict the probability of passing for a student who studied **3 hours**.

**Given:**
*   $x = 3$
*   $w = 1.5$
*   $b = -4$

### 3. Step-by-Step Calculation

**Step A: Calculate the Linear Combination ($z$)**
First, we combine the input and weights linearly.
$$z = (w \times x) + b$$
$$z = (1.5 \times 3) + (-4)$$
$$z = 4.5 - 4$$
$$z = 0.5$$

**Step B: Apply the Sigmoid Function**
Now, we pass $z$ through the sigmoid function to convert it into a probability between 0 and 1.

$$P(Y=1 | X) = \sigma(z) = \frac{1}{1 + e^{-z}}$$

Substitute $z = 0.5$:
$$P = \frac{1}{1 + e^{-0.5}}$$

Calculate the exponent ($e^{-0.5} \approx 0.6065$):
$$P = \frac{1}{1 + 0.6065}$$
$$P = \frac{1}{1.6065}$$
$$P \approx 0.622$$

### 4. Interpretation
*   **Probability:** The model predicts there is a **62.2%** chance the student will Pass.
*   **Class Label:** Since $0.622 > 0.5$ (the standard threshold), we classify this as **Pass (1)**.

### 5. Comparison of Outcomes
To see the effect of the linear combination, let's check a student who studied **1 hour**.

**Calculate $z$:**
$$z = (1.5 \times 1) - 4 = -2.5$$

**Apply Sigmoid:**
$$P = \frac{1}{1 + e^{2.5}} \approx \frac{1}{1 + 12.18} \approx \frac{1}{13.18} \approx 0.076$$

*   **Result:** **7.6%** probability.
*   **Class Label:** Since $0.076 < 0.5$, we classify as **Fail (0)**.