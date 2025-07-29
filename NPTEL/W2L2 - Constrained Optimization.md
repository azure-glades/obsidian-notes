
## Introduction to Optimization

- **Objective:** To find the optimal (maximum or minimum) value of a function, often referred to as the **objective function**.
    
- **Economic Applications:** Optimization is fundamental in economics, e.g., resource allocation, utility maximization, cost minimization.
    
- **Minimization vs. Maximization:**
    - Most mathematical techniques are framed as minimization problems.
    - A maximization problem can be converted to a minimization problem by taking the negative of the objective function.
- **Optimization Techniques:**
    - **Analytical Methods:** Based on differentiation and equating to zero (e.g., finding critical points).
    - **Numerical Methods:** Iterative approaches starting with an initial solution and moving step-by-step towards the optimum (e.g., **Gradient Descent**).
        
- **Unconstrained vs. Constraint Optimization:**
    - **Unconstrained Optimization:** No restrictions on the solutions. Techniques like gradient descent work well here.
    - **Constraint Optimization:** Solutions must satisfy specific conditions or **constraints**. This is more complex because the optimal unconstrained solution might not be _feasible_ (i.e., it might violate constraints).
        

---

## Constraint Optimization Problem

- **Definition:** Minimizing or maximizing an objective function subject to one or more restrictions on the variables.
    
- **Core Idea:** Not all possible solutions are acceptable; only those within a **feasible region** are considered.
    
- **Example: Resource Allocation**    
    - **Objective:** Maximize net revenue or utility by allocating resources to different sectors.
    - **Constraints:**
        - **Budgetary Limit:** Total resources available for investment are limited.
            
        - **Specific Sector Limits:** A particular sector might have a maximum allocation.
            
        - **Fairness Constraints:** E.g., no sector receives more than twice the resources of another.
            
- **Impact of Constraints:** The optimal solution under constraints might yield a lower objective function value than the unconstrained optimum, but it's the best possible given the limitations.
    

---

## Constraint Linear Optimization (Linear Programming)

- **Characteristics:**
    - **Objective Function:** A **linear function** (P=c1​x1​+c2​x2​+⋯+cn​xn​).
    - **Constraints:** Also **linear**, typically in the form of inequalities (e.g., aij​xj​≤bi​) and non-negativity constraints for variables (xj​≥0).
        
- **Converting Inequalities to Equations: Slack Variables**
    - An inequality like LHS≤RHS can be converted to an equality by adding a **non-negative slack variable** (s) to the LHS: LHS+s=RHS.
    - Each inequality constraint requires a unique slack variable.
    - This transforms a system of inequalities into a system of linear equations.
        
- **Basic Solution:** In a linear program with n decision variables and m constraints (after converting to equations with slack variables, total m+n variables and m equations), a basic solution is one where at least n of the variables are set to 0.
    
- **Basic Feasible Solution:** A basic solution that also satisfies all the original constraints (i.e., corresponds to a point within the feasible region).
    
    - Graphically, these often represent the **corner points** or vertices of the feasible region (a polygon or polyhedron).
        

### Fundamental Theorem of Linear Programming

- **Statement:** If an optimal solution to a linear programming problem exists, then at least one optimal solution must occur at one or more of the **basic feasible solutions** (i.e., corner points) of the feasible region.
    
- **Implication:** Instead of evaluating the objective function across the entire feasible region, we only need to evaluate it at the finite number of basic feasible solutions. The one yielding the best objective function value is the solution.
    
- **Example:** For a 2D problem, if the feasible region is a quadrilateral, the optimal solution will be one of its four corner points.
    

---

## Lagrange Multipliers

- **Application:** Used for optimization problems with **equality constraints**, and can be extended to inequality constraints. Applicable even when the objective function or constraints are **non-linear**.
    
- **Problem Formulation (Equality Constraints):**
    - Minimize f(x) subject to $h_j​(x)=0 \text{ for } j=1,…,k.$
        
- **Augmented Objective Function (Lagrangian):**
    - Construct a new function $$L(x,λ)=f(x)+∑_{j=1}^k​λ_j​h_j​(x)$$
        
    - λ=(λ1​,…,λk​) are the **Lagrange multipliers**, which are additional variables introduced.
        
- **Solving the Problem:**
    - Treat the Lagrangian as an unconstrained minimization problem.
        
    - Find the **stationary points** by setting the partial derivatives of L with respect to all variables (x and λ) to zero.
        
- **Lagrange Multiplier Theorem:** The stationary points of the augmented Lagrangian function correspond to the solutions of the original constrained optimization problem.
    

### Handling Inequality Constraints (Karush-Kuhn-Tucker (KKT) Conditions)

- **Problem Formulation:**
    - Minimize f(x)
    - Subject to:
        - hj​(x)=0 (Equality Constraints)
            
        - gi​(x)≤0 (Inequality Constraints - _Correction: original transcript had a typo, this is the correct form_)
            
- **Augmented Objective Function:** Similar to before, but inequality constraints are first converted to equalities using slack variables, and then incorporated. This results in two sets of Lagrange multipliers: one for original equality constraints and one for converted inequality constraints.
    
- **KKT Conditions:** A set of necessary conditions that a solution to a non-linear constrained optimization problem must satisfy.
    1. **Stationarity:** $∇L(x,λ,μ)=0$ (gradient of the augmented Lagrangian with respect to all variables, including slack variables, is zero).
        
    2. **Primal Feasibility:** All constraints are satisfied: hj​(x)=0 and gi​(x)≤0.
        
    3. **Complementary Slackness:** For each inequality constraint gi​(x)≤0 and its corresponding Lagrange multiplier μi​, the condition μi​gi​(x)=0 must hold. This implies either the constraint is binding (gi​(x)=0) or its multiplier is zero (μi​=0).
        
    4. **Dual Feasibility (Sign Condition):** The Lagrange multipliers associated with inequality constraints must be non-negative: μi​≥0.
        

---

## Interior Point Methods

- **Core Idea:** Start with an initial solution that is **within the feasible region** (satisfies all constraints) and iteratively move towards the optimal solution while always staying inside the feasible region.
    
- **Challenge:** Ensuring that each step taken to improve the objective function doesn't violate any constraints.
    
- **Solution: Barrier Function:**
    - An **augmented objective function** is created by adding a **barrier function** B(x) to the original objective function f(x). $$L_{\text{augmented​}}(x,μ)=f(x)+μB(x).$$
        
    - The barrier function takes a **high value** for points **outside** the feasible region and **low values** for points **inside**.
        
    - This "penalizes" movement outside the feasible region, effectively forcing the optimization algorithm to stay within bounds.
        
- **Parameter μ (Barrier Coefficient):**
    
    - Controls the importance given to the barrier function.
        
    - Start with a **high μ** to strongly prevent leaving the feasible region.
        
    - **Gradually decrease μ** over iterations. This allows the algorithm to prioritize optimizing the original objective function more as it gets closer to the optimum within the feasible region.
        
    - The goal is to approach the original unconstrained problem as μ→0.
        

---

## Exterior Point Methods

- **Core Idea:** Start with an initial solution that may be **outside the feasible region** (violates some constraints). The algorithm then iteratively moves the solution towards the feasible region while simultaneously optimizing the objective function.
    
- **Solution: Penalty Function:**
    - An **augmented objective function** is created by adding a **penalty function** to the original objective function.
        
    - The penalty function imposes a "cost" for violating constraints. The greater the violation, the higher the penalty.
        
    - **Gradually increase the weight** (analogous to μ in interior point methods) of the penalty function over iterations. This progressively pushes the solution towards satisfying the constraints.
        
- **Distinction from Interior Point:** Interior point methods aim to stay within the feasible region from the start, while exterior point methods start outside and try to converge into the feasible region.
    

---