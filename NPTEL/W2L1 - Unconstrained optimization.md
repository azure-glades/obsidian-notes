
## 1. Introduction to Optimization in Economics

### 1.1 Basic Economic Optimization Problem

**Scenario**: Government budget allocation between sectors

- **Budget**: M (total available funds)
- **Sectors**: Education (S₁) and Healthcare (S₂)
- **Investment amounts**: x in education, (M-x) in healthcare

**Performance Functions**:

- **f₁(x)**: Performance measure for education (e.g., college graduates per year)
- **f₂(M-x)**: Performance measure for healthcare (e.g., life expectancy)
- **Assumption**: Higher values are better for both functions

**Utility Function**: F(x) = f₁(x) + f₂(M-x)

- **Objective**: Maximize utility with respect to x
- **Method**: Use calculus - set dF/dx = 0 and solve

### 1.2 Multivariable Extension

**Enhanced Problem**:

- **Utility Function**: F(x₁,x₂) = f₁(x₁) + f₂(x₂)
- **Constraint**: x₁ + x₂ ≤ M (don't need to spend entire budget)
- **Degrees of Freedom**: 2 (both x₁ and x₂ can vary independently)

**Indifference Curves**:

- **Definition**: Curves connecting points with equal utility values
- **Example**: If f₁(2) + f₂(2) = 4 and f₁(1) + f₂(4) = 4, then (2,2) and (1,4) lie on same indifference curve
- **Interpretation**: All solutions on same curve are equivalent

## 2. Optimization Methodology

### 2.1 General Approach

**Standard Form**: Convert all problems to **minimization**

- If maximizing f(x), minimize -f(x)
- **Example**: Linear regression minimizes least squares error: Σ(yᵢ - wxᵢ - b)²

**Analytical vs. Numerical Methods**:

- **Analytical**: Use calculus (∂f/∂w = 0, ∂f/∂b = 0) for closed-form solutions
- **Numerical**: Use iterative algorithms when analytical solutions impossible

### 2.2 Gradient Descent Algorithm

**Basic Algorithm**:

```
1. Start with initial point x₀
2. Update: x₁ = x₀ - α × (df/dx)|ₓ₀
3. Repeat until convergence: xₙ₊₁ = xₙ - α × (df/dx)|ₓₙ
4. Stop when xₙ₊₁ ≈ xₙ
```

**Key Parameters**:

- **α (Learning Rate)**: Controls step size
- **Convergence Condition**: x₁ = x₀ (derivative = 0 at minimum)

**Example**: f(x) = x² - 4x + 4

- **Derivative**: f'(x) = 2x - 4
- **Optimal Solution**: x = 2 (where f'(x) = 0)
- **Algorithm**: Starting from x₀ = 5, α = 0.1
    - x₁ = 5 - 0.1 × (10 - 4) = 5 - 0.6 = 4.4
    - Continue until convergence at x = 2

### 2.3 Multivariable Case

**Vector-Valued Variables**: x = [x₁, x₂, ..., xₐ]

- **Gradient**: ∇f = [∂f/∂x₁, ∂f/∂x₂, ..., ∂f/∂xₐ]
- **Update Rule**: x₁ = x₀ - α∇f|ₓ₀

**Coordinate Descent**: Update one dimension at a time

1. Fix x₂, x₃, ..., xₐ, optimize x₁
2. Fix x₁, x₃, ..., xₐ, optimize x₂
3. Continue for all dimensions

## 3. Learning Rate and Convergence

### 3.1 Learning Rate Effects

**Large Learning Rate (α)**:

- **Advantage**: Fast convergence
- **Risk**: May overshoot minimum, causing oscillation
- **Problem**: Algorithm may never converge

**Small Learning Rate (α)**:

- **Advantage**: Guaranteed convergence (if function is well-behaved)
- **Disadvantage**: Slow convergence, many iterations required

### 3.2 Newton-Raphson Method

**Update Rule**: x₁ = x₀ - f(x₀)/(f'(x₀))

**Advantages**:

- Faster convergence than gradient descent
- No learning rate parameter needed

**Disadvantages**:

- For vectors: requires Hessian matrix inversion
- Computational complexity increases significantly
- May have numerical stability issues

## 4. Convex vs. Non-Convex Functions

### 4.1 Convex Functions

**Definition**: For any two points x₁, x₂ and any point x between them: f(x) ≤ Linear interpolation between f(x₁) and f(x₂)

**Properties**:

- **Unique minimum**: Only one global minimum exists
- **Guaranteed convergence**: Gradient descent will find global minimum
- **No local minima**: Any minimum found is the global minimum

### 4.2 Non-Convex Functions

**Properties**:

- **Multiple local minima**: Several "valleys" in the function
- **Convergence dependency**: Algorithm converges to nearest local minimum
- **Initial point importance**: Starting location determines final solution

**Strategy for Non-Convex Problems**:

1. Start from multiple different initial points
2. Find local minimum for each starting point
3. Compare all local minima found
4. Select the best (global minimum among local minima)

## 5. Multi-Objective Optimization

### 5.1 Problem Definition

**Example**: Flight selection problem

- **Objectives**: Minimize both time and cost
- **Airlines Data**:
    
    |Airline|Time (hrs)|Cost (₹000s)|
    |---|---|---|
    |Indigo|2|8|
    |GoAir|3|8|
    |Vistara|3|6|
    |Air Asia|4|5|
    

### 5.2 Dominance Concept

**Solution x₁ dominates x₂** if:

- f_i(x₁) ≤ f_i(x₂) for all objectives i (assuming minimization)
- f_j(x₁) < f_j(x₂) for at least one objective j

**Examples from flight data**:

- **Indigo dominates GoAir**: Same cost, less time
- **Air Asia dominates Jet Airways**: Same time, less cost
- **No dominance between GoAir and Vistara**: GoAir faster but more expensive

### 5.3 Pareto Optimality

**Pareto Optimal Solution**: Not dominated by any other solution

- Cannot improve one objective without worsening another
- **Pareto Optimal Set**: Collection of all Pareto optimal solutions

**Ranking System**:

- **Rank 1**: Pareto optimal solutions (not dominated by anyone)
- **Rank 2**: Solutions dominated only by Rank 1 solutions
- **Rank 3**: Solutions dominated only by Rank 1 and 2 solutions

**Pareto Front**: Boundary in objective function space defined by Pareto optimal solutions

### 5.4 Solution Approaches

**Weighted Sum Method**:

- Combine objectives: F = w₁f₁ + w₂f₂ + ... + wₙfₙ
- Weights reflect priorities/importance
- Convert multi-objective to single-objective problem
- **Limitation**: May miss some Pareto optimal solutions

**Goal**: Find diverse Pareto optimal solutions

- Each solution excels in different objectives
- Provides decision-maker with range of trade-off options

## 6. Economic Applications

### 6.1 Resource Allocation

- **Budget distribution** among multiple sectors
- **Performance trade-offs** between different priorities
- **Utility maximization** subject to constraints

### 6.2 International Trade

- **Comparative advantage**: Countries specialize in efficient production
- **Trade optimization**: Maximize benefits for all parties
- **Multi-criteria decisions**: Cost, quality, strategic importance

### 6.3 Income Distribution

- **Wealth redistribution**: From wealthy to poor individuals
- **Social welfare maximization**: Improve overall societal well-being
- **Pareto improvements**: Help some without hurting others

### 6.4 Policy Making

- **Multi-stakeholder decisions**: Balance competing interests
- **Trade-off analysis**: Understand costs and benefits
- **Optimal policy selection**: Choose best among feasible alternatives

## Key Concepts and Formulas

### Optimization Formulas

- **Gradient Descent**: x₁ = x₀ - α∇f(x₀)
- **Newton-Raphson**: x₁ = x₀ - f(x₀)/f'(x₀)
- **Convergence Condition**: ∇f(x*) = 0

### Multi-Objective Concepts

- **Dominance**: x₁ ≺ x₂ if f_i(x₁) ≤ f_i(x₂) ∀i and ∃j: f_j(x₁) < f_j(x₂)
- **Weighted Sum**: F = Σ wᵢfᵢ(x)
- **Pareto Optimal**: No solution dominates it

## Important Terms

- **Utility Function**: Measures overall benefit/satisfaction
- **Indifference Curve**: Points with equal utility values
- **Learning Rate (α)**: Step size in gradient descent
- **Gradient (∇f)**: Vector of partial derivatives
- **Hessian Matrix**: Matrix of second-order partial derivatives
- **Convex Function**: Has unique global minimum
- **Local Minimum**: Lowest point in neighborhood
- **Global Minimum**: Lowest point overall
- **Pareto Optimal**: Non-dominated solution
- **Pareto Front**: Boundary of optimal trade-offs
- **Dominance**: One solution better than another in all aspects


[[W2L2 - Constrained Optimization]]