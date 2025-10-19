### Interventional Causality and Attribution

This lecture expands on the concept of causality, moving beyond simple correlation and introducing the idea of **interventional causality** and how it can be modeled and measured. It explores how machine learning techniques can be used to understand cause-and-effect relationships in economic scenarios.

---

### 1. Interventional Causality

* **Core Idea:** To truly establish causality, we must observe the impact of a deliberate **intervention** on a system while keeping all other conditions constant.
* **Controlled Experiments:** The ideal way to measure causality is through controlled experiments where a "treatment" variable is changed manually to see its effect on a "target" variable.
* **Limitation of Granger Causality:** Naive approaches like Granger causality, which rely on observational data, cannot account for **confounders**—hidden variables that influence both the treatment and the target, creating a spurious correlation.
* **The "Do" Operator:** This concept is represented mathematically by the "do" operator, as in $P(y | \text{do}(x))$, which signifies that the value of $x$ is being forced or intervened upon, breaking any natural dependencies it had with other variables.
* **The Challenge:** Many real-world interventions are either **unethical** (e.g., forcing people to smoke to study cancer) or **infeasible** (e.g., artificially heating a region of the ocean).

### 2. Randomized Control Trials (RCTs)

* **Definition:** "A principled way to pull out the causal effects of a treatment that can take $k$ possible values."
* **Method:**
    1.  Divide a population into $k$ **homogeneous groups** (statistically identical in terms of all relevant attributes).
    2.  Apply a different treatment value ($x_1, x_2, \dots, x_k$) to each group.
    3.  Measure the impact on the target variable ($y$) across all groups.
* **Advantage:** By ensuring the groups are homogeneous, any observed difference in the target variable can be confidently attributed to the intervention, as the influence of confounding variables is minimized.
* **Applications in Economics:** RCTs are widely used in developmental economics (e.g., studying the impact of microfinance schemes), labor economics, and public policy. Abhijit Banerjee and Esther Duflo won the Nobel Prize for their work using this methodology.

---

### 3. Counterfactuals and Structural Causal Models

* **Counterfactuals:** Scenarios that are contrary to what actually happened. For example, "What would the temperature be today **if** industrialization had not occurred?"
* **Challenge:** It is impossible to directly observe or intervene on counterfactuals.
* **Structural Causal Models (SCMs):**
    * A mathematical framework for representing causal relationships using a set of equations.
    * These equations can be either **deterministic** or **probabilistic**.
    * They allow for the simulation of counterfactual scenarios and interventions by explicitly modeling how variables influence each other.
* **Machine Learning's Role:** Predictive machine learning models can be used as a proxy for these structural equations to approximate a structural causal model.

---

### 4. Feature Attribution with Shapley Values

* **The Problem:** In a predictive model, we want to understand how each input feature contributes to the final prediction, especially when the prediction is different from the average.
* **Shapley Value:** A concept from game theory that quantifies the contribution of each member in a team. It's used in machine learning to attribute the outcome of a prediction to each input feature.
* **Attribution:** For a single data point, Shapley values can explain why a prediction was higher or lower than the expected average. For example, in a bicycle rental model, a high rental count could be attributed to a positive Shapley value for "good weather" and a negative one for "thunderstorms."
* **SHAP (SHapley Additive exPlanations):** An algorithm that provides a practical way to compute Shapley values for machine learning models.

---

### 5. Double Machine Learning (DoubleML)

* **The Problem:** We want to measure the causal impact of a treatment variable ($X$) on an outcome variable ($Y$) while accounting for a confounder ($D$) that influences both.
* **The Challenge:** Directly regressing $Y$ on $X$ and $D$ can lead to inconsistent results because of the collinearity between $X$ and $D$.
* **DoubleML Approach:** This method breaks the problem down into three separate regression tasks to isolate the true causal effect.
    1.  **Regress $X$ on $D$:** Predict the treatment from the confounders to get the residual ($v$). This residual represents the part of $X$ that is independent of the confounders.
    2.  **Regress $Y$ on $D$:** Predict the outcome from the confounders to get the residual ($w$). This residual represents the part of $Y$ that is independent of the confounders.
    3.  **Regress the residuals:** Regress the outcome residual ($w$) on the treatment residual ($v$). The resulting coefficient is the true causal effect, $\beta_2$, of the treatment on the outcome, now purged of the confounder's influence.
* **Benefit:** DoubleML allows machine learning models to be used for causal inference, providing a way to disentangle causation from confounding factors.