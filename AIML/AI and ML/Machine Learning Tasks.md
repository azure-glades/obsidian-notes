In machine learning, these terms are often used interchangeably in casual conversation, but they have precise technical differences. Think of them as a hierarchy, moving from a single data point to the entire model's goal
### Loss Function (The "Individual" Level)
The **loss function** measures how "wrong" the model is on a **single training example**. It calculates the penalty for a single prediction compared to the true label.
- **Goal:** To quantify the error for one specific input.
- **Example (Regression):** If you predict a house price is $\$300k$ but it’s actually $\$350k$, the "Squared Error" loss for that one house is $(350 - 300)^2 = 2500$.
- **Example (Classification):** Using "Hinge Loss" to see if a single image was correctly classified as a "Cat."
### Cost Function (The "Batch" Level)
The **cost function** is the average (or sum) of the loss functions over the **entire training dataset**. It represents the total error of the model across all data points it has seen.
- **Goal:** To provide a single number that reflects the model's overall performance.
- **Formula:** $Cost = \frac{1}{n} \sum_{i=1}^{n} Loss(y_i, \hat{y}_i)$
- **Example:** **Mean Squared Error (MSE)** is a cost function because it averages the squared losses of all houses in your dataset.
### Objective Function (The "Optimization" Level)
The **objective function** is the most general term. It is any function that you intend to **maximize or minimize** during optimization.
- **Relationship:** In most machine learning cases, the cost function _is_ the objective function (which we want to minimize).
- **Distinction:** An objective function doesn't always have to be a "loss." For example:
    - In Reinforcement Learning, the objective is a **Reward Function** (which you want to maximize).
    - In some models, the objective function is the **Cost Function + Regularization** (a penalty to prevent overfitting).

| **Term**               | **Scope**           | **Common Examples**                              |
| ---------------------- | ------------------- | ------------------------------------------------ |
| **Loss Function**      | Single data point   | Squared Error, Hinge Loss, Binary Cross-Entropy  |
| **Cost Function**      | Entire training set | Mean Squared Error (MSE), Log Loss               |
| **Objective Function** | The general goal    | MLE (Maximum Likelihood), Reward, Cost + Penalty |
Visualizing the Goal
Imagine you are playing golf.
- The **Loss** is how far a **single shot** landed from the hole.
- The **Cost** is your **average distance** from the hole for the entire 18-hole game.
- The **Objective** is the **final score** you want to minimize to win the tournament.

# Data Splits: Training, Validation, and Testing
Think of this like a student preparing for a final exam.
- **Training Set (The Textbook):** This is the data the model "sees" and learns from. It uses this to adjust its internal weights and biases. Typically, this is the largest portion of your data (e.g., **70–80%**).
- **Validation Set (The Practice Quiz):** This data is **not** used for training. Instead, it is used to evaluate the model frequently during development. It helps you decide which version of the model is best or which settings (hyperparameters) work best.
	- ***Simulates unseen data for model selection***
- **Testing Set (The Final Exam):** This data is held back until the very end. The model has **never seen** this data during training or tuning. It provides an unbiased report card on how the model will perform in the real world.
## The Order of Operations
The process follows a specific, logical sequence to prevent "data leakage" (where the model accidentally learns answers it shouldn't know yet).
1. **Training Phase:** You feed the **Training Set** to the model. The model learns patterns and adjusts its internal parameters.
2. **Validation Phase:** You run the **Validation Set** through the model. You look at the results and say, _"Wait, the accuracy is low; let me change the settings (hyperparameters) and try again."_ You repeat steps 1 and 2 until you are happy with the performance.
3. **Testing Phase:** Once you have "locked in" your final model, you run the **Testing Set** exactly **once**. This tells you the final accuracy. **You do not go back and change the model after this step.**

> See Further:
> [[Hyperparameters]] 
> [[Performance Measure]] 
> [[Overfitting and Underfitting]]

> Types of machine learning:
> [[Unsupervised Learning]], [[Supervised Learning]]

