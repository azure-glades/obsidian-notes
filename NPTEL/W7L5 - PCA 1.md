This lecture provides the essential mathematical prerequisites for understanding Principal Component Analysis (PCA), a technique used for dimensionality reduction. It covers four main topics: random vectors, vector differentiation, eigenvalues and eigenvectors, and Lagrange optimization.

***

### 1. Random Vectors

A **random vector** is a vector whose components are random variables. Just like a single random variable has an expectation and variance, a random vector has an expectation and a covariance matrix.

* **Expectation:** The expectation of a random vector is simply a vector containing the expectations of each of its random variables.
    * $E[X] = E\begin{bmatrix} X_1 \\ X_2 \\ \vdots \\ X_n \end{bmatrix} = \begin{bmatrix} E[X_1] \\ E[X_2] \\ \vdots \\ E[X_n] \end{bmatrix} = \begin{bmatrix} \mu_1 \\ \mu_2 \\ \vdots \\ \mu_n \end{bmatrix}$

* **Variance:** The variance of a random vector is a matrix, known as the **covariance matrix**, denoted by $\Sigma$. This matrix captures not only the variance of each individual variable but also the covariance between every pair of variables.
    * $\text{Var}(X) = \Sigma = E[(X - \mu)(X - \mu)^T]$
    * The diagonal elements of the covariance matrix, $\Sigma_{ii}$, are the variances of the individual random variables, $\text{Var}(X_i)$.
    * The off-diagonal elements, $\Sigma_{ij}$, are the covariances between the random variables, $\text{Cov}(X_i, X_j)$.

***

### 2. Vector Differentiation

Vector differentiation is the process of finding the derivative of a function with respect to a vector.

* **Gradient:** The derivative of a scalar function $f(x)$ with respect to a vector $x = [x_1, x_2, ..., x_n]^T$ is a vector known as the **gradient**, denoted as $\nabla_x f$. It contains the partial derivatives of the function with respect to each component of the vector.
    * $\nabla_x f = \begin{bmatrix} \frac{\partial f}{\partial x_1} \\ \frac{\partial f}{\partial x_2} \\ \vdots \\ \frac{\partial f}{\partial x_n} \end{bmatrix}$

* **Key Results for PCA:** Two important vector differentiation results are:
    1.  The derivative of $a^T x$ with respect to $x$ is the vector $a$.
        * $\nabla_x (a^T x) = a$
    2.  The derivative of $x^T A x$ with respect to $x$ is $2Ax$, where $A$ is a symmetric matrix.
        * $\nabla_x (x^T A x) = 2Ax$

***

### 3. Eigenvalues and Eigenvectors

**Eigenvectors** are special vectors that, when multiplied by a matrix, only change in magnitude, not in direction. The scalar by which their magnitude changes is called the **eigenvalue**.

* **Definition:** For a square matrix $A$, an eigenvector $x$ and its corresponding eigenvalue $\lambda$ satisfy the equation:
    * $Ax = \lambda x$
* **Finding Eigenvalues:** Eigenvalues are found by solving the characteristic equation:
    * $\text{det}(A - \lambda I) = 0$
* **Geometric Intuition:** Pre-multiplying a vector by a matrix can rotate and stretch it. An eigenvector is a vector that only gets stretched or shrunk, but it doesn't get rotated by the matrix. 

***

### 4. Lagrange Optimization

Lagrange optimization is a method for solving **constrained optimization problems**, which involve maximizing or minimizing a function subject to one or more constraints.

* **The Lagrangian:** The method introduces a new variable, the **Lagrange multiplier ($\lambda$)**, to combine the objective function and the constraints into a single function called the Lagrangian.
    * To maximize $f(x, y)$ subject to $g(x, y) = c$, we form the Lagrangian:
        * $\mathcal{L}(x, y, \lambda) = f(x, y) - \lambda(g(x, y) - c)$
* **Solving the Problem:** The solution is found by taking the partial derivatives of the Lagrangian with respect to each variable and the Lagrange multiplier, and setting them all to zero. This creates a system of equations that can be solved to find the optimal values.