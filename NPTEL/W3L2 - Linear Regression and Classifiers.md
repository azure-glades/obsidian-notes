## Keywords and Definitions
* **Feature Space:** A **feature space** is an abstract, multi-dimensional space where each dimension corresponds to a different **feature** or attribute of the data."The space that a feature vector belongs to." 
	* For example, if you're analyzing a car, the features might be its `engine size`, `fuel efficiency`, and `price`. The feature space would be a 3D space, and a specific car with values (2.0L, 15 km/L, $25,000) would be a point located at these coordinates.

* **Label Space:**  A **label space** is the set of all possible output values that a machine learning model can predict. "The space that a label vector belongs to."
	* **For a classification problem**, the label space is a set of discrete, finite categories. For instance, in a model that identifies animals in a photo, the label space might be {cat, dog, bird}.
	- **For a regression problem**, the label space is a continuous range of values. For example, in a model that predicts a house price, the label space could be all positive real numbers, say from $100,000 to $5,000,000.

* **Classification:** "The problem where the label space is discrete." -> the goal is to predict what class an input falls into.
* **Regression:** "The problem where the label space is continuous or real-valued." -> the goal is to predict a **continuous** output value based on input features

* **Training Data:** "The data provided for calibration."
* **Linearly Separable:** A dataset is **linearly separable** if it's possible to perfectly divide the data points of two different classes using a single straight line, plane, or hyperplane. It means there is a linear classifier that is 100% accurate.

### Supervised Learning: Linear Regression and Classifiers
#### 1. Introduction to Supervised Learning
* **Goal:** To learn a function, $f$, that maps a feature vector ($x$) to a label ($y$).
* **Data:** Training data consists of labeled observations, $(x_1, y_1), \dots, (x_n, y_n)$.
* **Function F:** Can be an explicit mathematical formula (e.g., polynomial) or an implicit algorithm (e.g., decision tree).
* **Problem Types:**
    * **Classification:** The label space is discrete (e.g., cat/dog).
    * **Regression:** The label space is continuous or real-valued (e.g., price, rating).

#### 2. General Approach for Supervised Learning
* **Hypothesis:** Make an assumption about the form of the function $f$.
* **Calibration (Training):**
    * Use training data to find optimal parameter values for the function $f$.
    * A "loss function" measures the discrepancy between the true label ($y$) and the predicted label ($f(x)$).
    * The goal is to **minimize the total loss** over all training examples.
* **Validation:** Test the calibrated model on new data to see how well it performs.

>[!note] Loss Function
>A **loss function** measures how well a machine learning model is performing. 📉 It quantifies the discrepancy between the model's predicted output and the true, actual output. The goal of training a model is to **minimize this loss**.
>For example:
>* In linear regression, a common loss function is the **squared error loss**. It calculates the squared difference between the predicted value and the true value, summing it up over all data points. This forces the model to reduce both positive and negative errors.
>* In classification, a loss function might be a simple count of misclassifications, called **0-1 loss**.
### 3. Linear Regression
* **Hypothesis:** The simplest assumption for the function $f$ is a linear model.
    * $f(x) = w^T x + w_0$ (where $w_0$ is a bias term).
    * This is a hyperplane in higher dimensions or a straight line in 2D.
* **Loss Function:** A common choice is the **squared error loss**, which squares the difference between the true and predicted values to prevent positive and negative errors from canceling out.
* **Application Example:** Predicting a product's overall rating ($y$) as a weighted average of its features ($x$). The weights, $w$, represent the importance of each feature.
* **Parameter Estimation:** The optimal weight vector $w$ can be found by minimizing the total squared error loss. The closed-form solution is:
    $w = (X^T X)^{-1} X^T y$
    (where $X$ is a matrix of feature vectors and $y$ is a vector of true labels).

---

### 4. Sparsity and Regularization
* **Problem:** Having too many features can make the model complex and difficult to estimate. In reality, only a few features might be important.
* **Sparsity:** The concept of a weight vector $w$ where most of the elements are zero. This indicates that only a few features are relevant for the prediction.
* **Regularization:** A technique to explicitly impose a desired structure on the parameter vector $w$.
* **Lasso Regression:** A method that adds a regularization term to the loss function to encourage sparsity.
    * The loss function becomes: $Loss = \sum (y - w^T x)^2 + \lambda ||w||_1$
    * The $||w||_1$ is the L1 norm of the weight vector.
    * The parameter $\lambda$ controls the trade-off between minimizing prediction error and achieving sparsity. A higher $\lambda$ leads to a sparser $w$ but may increase prediction error.
    * Lasso is an acronym for "Least Absolute Shrinkage and Selection Operator."

> [!NOTE] Sparsity
> This describes a situation where a model's parameter vector (like the weight vector **w** in linear regression) has many zero values. When a model is sparse, it means it's only using a small number of features to make its predictions, effectively ignoring the rest. This simplifies the model and makes it more interpretable.

> [!NOTE] Regularization
> This is a technique used to impose a specific structure on a model's parameters, often to encourage sparsity and prevent **overfitting**. It does this by adding a penalty term to the loss function. This penalty increases the loss if the parameters have undesirable properties (e.g., being too large or too numerous).

### How Do You Choose a Weight Vector?

The weight vector is chosen by **minimizing the loss function** over the training data. This is typically done through an optimization process.

For a simple linear regression model, you can find the optimal weight vector **w** by taking the derivative of the total loss function with respect to **w**, setting it to zero, and solving the resulting equation. This gives you a closed-form solution.

In more complex cases, or when a regularizer is added, an iterative optimization algorithm (like gradient descent) is used to gradually adjust the weights to reduce the loss.

### What is Lasso Regression?
**Lasso Regression** is a type of linear regression that combines the standard squared error loss with a penalty on the **L1 norm** of the weight vector.  This penalty term encourages the model to use fewer features by driving the weights of unimportant features to zero, thus promoting sparsity. It's a powerful technique for both regularization and **variable selection**.
The optimization problem for Lasso is to minimize:

$$\text{Loss} = \sum_{i=1}^{n} (y_i - w^T x_i)^2 + \lambda ||w||_1$$

where $\lambda$ is a parameter that controls the strength of the penalty. A larger $\lambda$ forces more weights to become zero, leading to a sparser model.


---

### 5. Linear Classification
* **Task:** To classify data points into two classes, e.g., +1 and -1 (binary classification).
* **Hypothesis:** A linear classifier attempts to separate the data points with a line (in 2D) or a hyperplane (in higher dimensions).
* **Prediction:** The model predicts the class based on the sign of a linear function: $y = \text{sign}(w^T x)$.
* **Linearly Separable Dataset:** "If there exists a linear classifier that achieves 100% accuracy."
* **Challenges:**
    * A simple linear classifier may not be the most stable.
    * There can be multiple linear classifiers that perfectly separate the data. We want the best one.
* **Perceptron Algorithm:** A simple algorithm that iteratively updates the weight vector $w$ whenever a misclassification occurs. It's guaranteed to find a solution if the dataset is linearly separable.
* **Max Margin Classifier:** A preferred linear classifier that is as far as possible from the data points of both classes. This makes it more robust to noise.
* **Support Vector Machine (SVM):** An algorithm used to find the max margin linear classifier.

> [!NOTE] Perceptron
>  This is a simple algorithm that finds *any* linear classifier that perfectly separates the data, if one exists. It works iteratively: if a data point is misclassified, the hyperplane's weights are adjusted to move it closer to the correct classification. The process stops once all data points are correctly classified. It's guaranteed to converge for a **linearly separable** dataset.

> [!NOTE] Support Vector Machine (SVM) 
> This is a more advanced algorithm that finds the **optimal** linear classifier, known as the **max-margin classifier**. Instead of just finding any separating line, SVM finds the one that has the largest possible distance (the margin) to the nearest data points of both classes.  This makes the classifier more robust and less sensitive to noise or small changes in the data. The data points that lie on the margin are called **support vectors**.

---

### 6. Applications in Economics
* **Financial Risk Assessment:** Linear models are used for forecasting economic parameters like GDP growth based on various indicators.
* **Variable Selection:** Using Lasso regression, a model can identify which economic indicators are truly relevant for a forecast, providing better predictions and economic insights.
