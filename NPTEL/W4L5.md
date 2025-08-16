### Causality in Time Series

This lecture explores the notion of causality, how it differs from correlation, and how we can identify it in time series data. It focuses on the **Granger causality** test and its limitations, as well as more advanced methods.

---

### Causality vs. Correlation

* **Causality:** The value of one variable, a "treatment" variable ($X$), directly influences the value of another, an "outcome" variable ($Y$). A change in $X$ causes a change in $Y$.
    * **Example:** Clouds cause rainfall. Smoking causes cancer.
    * **Question:** If the value of $Y$ changes, how much of that change can be attributed to the change in $X$?
* **Correlation:** Two variables change together, but this does not necessarily mean one causes the other.
* **The Distinction:** Correlation does not imply causation. Even if two variables exhibit a high correlation, it does not guarantee a causal relationship. The reverse, however, may be true: if a causal relationship exists, there should be some form of correlation, possibly with a time lag.
* **Spurious Correlation:** A situation where two variables have a high correlation coefficient, but there is no actual causal link between them.
    * **Example 1:** US spending on science and technology is highly correlated with the number of suicides. This is a **spurious correlation** as one does not cause the other.
    * **Example 2:** Ice cream sales are correlated with shark attacks. This is also spurious, likely caused by a **confounding variable** like **temperature**.
* **Confounding Variables:** A third variable that influences both the treatment and the outcome variables, creating an apparent correlation that is not a true causal link. In economics, this is a major challenge in determining causality (e.g., is a person's high income due to education or being born into a wealthy family?).

---

### Types of Causality

* **Bidirectional Causality:** A situation where $X$ influences $Y$, and $Y$ also influences $X$.
    * **Self-Destructive Process:** A positive causal relation from $X$ to $Y$ and a negative causal relation from $Y$ to $X$.
        * **Example:** Higher temperature ($X$) causes more rainfall ($Y$), but more rainfall causes a decrease in temperature.
    * **Self-Replenishing Process:** A positive causal relation from $X$ to $Y$ and a positive causal relation from $Y$ to $X$.
        * **Example:** Higher temperature ($X$) leads to more use of air conditioners ($Y$, which release greenhouse gases), which in turn causes the temperature to rise further.

---

### Granger Causality

* **Definition:** "If the past values of one time series ($X$) can be used to predict the future values of another time series ($Y$) better than using only the past values of $Y$ itself, then we say that $X$ **Granger causes** $Y$."
* **Method:**
    1.  **Model M1:** A simple **autoregressive model** that predicts the present value of $Y$ based only on its own past values.
    2.  **Model M2:** A more complex model that predicts the present value of $Y$ based on its own past values AND the past values of $X$.
    3.  **Comparison:** If the prediction error of M2 is significantly less than the error of M1, we conclude that $X$ Granger causes $Y$.
* **Bidirectional Test:** The process can be reversed to check if $Y$ Granger causes $X$.
* **Applications in Economics:**
    * **GDP vs. CO2:** Granger causality has been used to study whether economic growth (GDP) causes an increase in carbon dioxide emissions.
    * **FDI vs. GDP:** It can analyze if Foreign Direct Investment (FDI) leads to an increase in a country's GDP.
* **Drawbacks of Granger Causality:**
    1.  **Assumes Linearity:** It traditionally relies on linear regression models. This can be mitigated by using non-linear models like neural networks.
    2.  **Cannot Handle Confounders:** It cannot detect the presence of confounding variables that are causing the observed correlation.
    3.  **Cannot Handle Contemporaneous Causality:** It cannot determine a causal relationship between two variables at the same time step ($X_t$ and $Y_t$) because it relies on the principle that the past can cause the future, but not vice versa.

---

### Other Methods: Conditional Independence

* **PC Algorithm:** An alternative method based on the statistical concept of **conditional independence**.
* **Mechanism:** It builds a causal graph by performing statistical tests to see if variables are independent of each other after conditioning on other variables. If a test shows they are conditionally independent, the link between them is removed. The remaining links indicate a causal relationship.
* **Advantages:** The PC algorithm is able to handle contemporaneous relations and can, in some cases, help identify confounders, addressing some of the key limitations of Granger causality.

### Keywords and Definitions

* **Granger Causality:** "A time series $X$ Granger causes another time series $Y$ if the past values of $X$ can improve the prediction of future values of $Y$ better than using only the past values of $Y$."
* **Confounding Variables:** "A third variable that influences both a treatment and an outcome, creating a spurious correlation that is not a true causal link."
* **Spurious Correlation:** "A high correlation between two variables that is not due to a causal relationship."
* **Autocorrelation:** "The property of a time series where its current values have some correlation with its past values."
* **Contemporaneous Causal Relations:** "A causal relationship between two variables that occur at the same time step."
* **Conditional Independence:** "A statistical notion that tests whether two variables are independent of each other after accounting for the influence of a third variable."