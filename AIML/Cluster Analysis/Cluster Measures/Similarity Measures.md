***Similarity Measure:*** Quantifies how similar two data points are to each other

***Dissimilarity Measure:*** Quantifies how different two data points are to each other. (Usually referred to as the *distance* between 2 points)


Similarity and dissimilarity measures differ based on the type of attribute

## Interval-Scaled Variables (Continuous)
These are linear, numerical values like weight, temperature, or price.
- **Distance** is used as the dissimilarity measure for interval scaled variables
    - *Euclidean:* Straight-line distance. - L2 norm
    - *Manhattan:* sum of absolute differences. - L1 norm
    - ***Minkowski:*** The mathematical generalization that encompasses both. - Lp norm

- *Standardization* is done to scale all the variables to the same axis. Prevents smaller magnitude variables from having small distances.
	- Standardization done via **Z Score**. For a variable $x$ , the z score for observation $x_i$ is $$z_i = \frac{x_i - \mu_i}{\sigma_z}$$
	- The variable now has mean = 0, standard dev = 1



## Binary Variables
A binary variable has only two possible states, typically coded as 0 and 1.
- **0** often means “absent” or “no”  
- **1** often means “present” or “yes”
But the interpretation of 0 and 1 determines whether the variable is symmetric or asymmetric.

| Type           | Meaning                                                                                           | Example                                                                                                                               |
| -------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **Symmetric**  | Both states (0 and 1) are equally important. The values carry the same weight.                    | Gender (male = 0, female = 1). neither value is “more significant” than the other.                                                    |
| **Asymmetric** | One state (usually **1 = present**) is more important or informative than the other (0 = absent). | Disease test result (1 = positive, 0 = negative) — a positive result is rare and meaningful; negative is common and less informative. |
> In asymmetric cases, **co-occurrence of 1s is meaningful**, but co-occurrence of 0s (both absent) is **not** considered evidence of similarity.
### Contingency Table
When comparing two binary objects (e.g., patients, documents), we construct a **2×2 contingency table**:

|                 | **Object 2: 1** | **Object 2: 0** | **Total**             |
| --------------- | --------------- | --------------- | --------------------- |
| **Object 1: 1** | a               | b               | a + b                 |
| **Object 1: 0** | c               | d               | c + d                 |
| **Total**       | a + c           | b + d           | **n = a + b + c + d** |
Where:
- **a** = number of attributes where **both** objects = 1  
- **b** = Object 1 = 1, Object 2 = 0  
- **c** = Object 1 = 0, Object 2 = 1  
- **d** = both = 0

#### For Symmetric Binary Variables
- Treats **all matches (1-1 and 0-0) equally**
- Similarity:  Simple matching coefficient (i.e Rand statistic)
  $$
  \text{SMC} = \frac{a + d}{a + b + c + d}
  $$
- Dissimilarity: $d_{\text{sym}} = 1 - \text{SMC} = \frac{b + c}{a + b + c + d}$
#### For Asymmetric Binary Variables
- **Ignores** the **d** term (both 0s), because co-absence isn’t meaningful
- Similarity: *Jaccard Coefficient*
$$
  J = \frac{a}{a + b + c}
$$
- Dissimilarity:  $d_{\text{asym}} = 1 - J = \frac{b + c}{a + b + c}$

- Jaccard focuses **only on positive matches**
- Widely used in:
	- **Text mining** (documents as sets of words)
	- **Biology** (species presence/absence in ecological sites)
	-  **Market basket analysis** (items bought together)

> [!example]
> Suppose we have medical records for two patients, indicating presence (1) or absence (0) of 5 symptoms:
> 
> | Symptom        | Fever | Cough | Headache | Nausea | Rash |
> |----------------|-------|-------|----------|--------|------|
> | **Patient A**  | 1     | 0     | 1        | 0      | 1    |
> | **Patient B**  | 1     | 1     | 1        | 0      | 0    |
> 
> Construct contingency table:
> - **a** = both 1 → Fever, Headache → **a = 2**
> - **b** = A=1, B=0 → Rash → **b = 1**
> - **c** = A=0, B=1 → Cough → **c = 1**
> - **d** = both 0 → Nausea → **d = 1**
> Total attributes = 5
> #### Symmetric distance (SMC-based):
> - Similarity = (a + d) / (a + b + c + d) = (2 + 1)/5 = **0.6**
> - Distance = 1 – 0.6 = **0.4**
> #### Asymmetric distance (Jaccard-based):
> - Jaccard similarity = a / (a + b + c) = 2 / (2 + 1 + 1) = **2/4 = 0.5**
> - Jaccard distance = 1 – 0.5 = **0.5**
> Note: The **asymmetric distance is higher** because we **ignore the matching 0** (Nausea), which slightly reduces perceived similarity.


## Nominal Variables
A nominal variable is a categorical variable with **two or more unordered states**. Examples:
- Color: red, yellow, blue, green  
- Country: USA, India, Brazil  
- Blood type: A, B, AB, O  
A binary variable is just a nominal variable with **M = 2** categories.
### Simple Matching algorithm
This method is used when you want to compare two objects (i and j) across a set of p nominal attributes.
- **Similarity (s):** This is the ratio of the number of attributes that match (m) to the total number of attributes (p). $$s(i,j)= \frac{m}{p}​$$
- **Distance (d):** This represents the dissimilarity. It is the ratio of attributes that do **not** match. $d(i,j)=\frac{p-m}{p}$

> [!Example]
> Imagine comparing two people based on 3 nominal variables: **Eye Color, Favorite Sport, and City.**
> - **Person i:** `[Brown, Soccer, New York]`
> - **Person j:** `[Blue, Soccer, New York]`
> 
> 1. **Total variables (p):** 3
> 2. **Number of matches (m):** 2 (Soccer and New York match; Eye color does not)
> 3. **Distance:** $d(i,j)=\frac{3−2}{3}​=0.33$
> 4. **Similarity:** $s(i,j)=\frac{2}{3}​=0.33$
> 
### Binary Transformation (One-Hot Encoding)
Nominal vars can be converted to binary vars by grouping
- **The Process:** If a variable "Color" has M states (Red, Yellow, Blue, Green), you create 4 new binary columns.
- **The Result:** Each object gets a **1** for the state it possesses and a **0** for all others.
Once converted to binary, binary distance and similarity measures are used based on how they are treated
- **Symmetric Binary:** If both 0 and 1 are equally important (use Simple Matching).
- **Asymmetric Binary:** If the "1" state (presence) is more important than "0" (absence), often used in medical diagnosis or keyword matching (use **Jaccard Coefficient**).


## Ordinal Variables
Ordinal variable is a categorical variable with a meaningful hierarchy/rank.
- Ordinal variables are converted to continuous variables by normalizing them

Converting to interval-scaled/continuous variable
If you have an ordinal variable with $M_f$ states (e.g., Bronze, Silver, Gold, Platinum; so $M_f = 4$):
1. **Assign Ranks ($r_{if}$):** Replace each value with its *rank* from $\{ 1 ... M_f\}$
    - Bronze = 1, Silver = 2, Gold = 3, Platinum = 4.
2. Normalize to $[0, 1]$ ($z_{if}$): Use the formula to ensure all variables have equal weight regardless of how many states they have.    $$z_{if} = \frac{r_{if} - 1}{M_f - 1}$$
    - _Example:_ For "Silver" (rank 2) in a 4-state system: $z = \frac{2-1}{4-1} = \frac{1}{3} = 0.33$.

**Dissimilarity:** Use a standard distance measure on these $z$ values since it is now an interval scaled variable
-  **Euclidean Distance:** $\sqrt{\sum (z_{if} - z_{jf})^2}$
- **Manhattan Distance:** $\sum |z_{if} - z_{jf}|$


## Ratio Scaled variables
Ratio-Scaled Variables are a positive measurement on a nonlinear scale,  or approximately at exponential scale.
- Convert them to interval-scaled variables by applying an inverse transform.
Ex: If variable is exponetially growing, use a logarithm to convert it to interval-scaled. $y_i= \log x_i$

## Variables of Mixed type
A database with many features of different types. 

A weighted formula is used to describe combine their effects - called *Grover's Similarity Coefficient* $$d(i, j) = \frac{\sum_{f=1}^{p} \delta_{ij}^{(f)} d_{ij}^{(f)}}{\sum_{f=1}^{p} \delta_{ij}^{(f)}}$$
where
- **$d_{ij}^{(f)}$**: The distance between object $i$ and $j$ for a specific feature $f$.
- **$\delta_{ij}^{(f)}$ (Indicator/Weight)**: Usually $1$ if both objects have a value for feature $f$. It is $0$ if one or both are missing data, or if the feature is an asymmetric binary and both are $0$.
- **$p$**: The total number of features.
Essentially, it is a **weighted average** of the distances calculated for each individual feature.


$d_{ij}^{(f)}$ is calculated differently depending on the type of variable:
- For binary
	- **$d_{ij}^{(f)} = 0$**: If the values are the same ($x_{if} = x_{jf}$).
	- **$d_{ij}^{(f)} = 1$**: If the values are different.
- For interval-scaled, we use **normalized distance**.
- For ordinal or Ratio scaled, use the rank formula to convert to interval scaled, then use normalized distance

## Vector Objects
Vector objects are larger object-type irregular data, like text in a document, keywords, genetic sequences, micro-arrays etc. Seen in NLP, biological taxonomy, etc. Generally used similarity measures are:
1. *Cosine Measure:* $$S(\vec{x}, \vec{y}) = \frac {\vec{x} \cdot \vec{y}}{\| \vec{x} \| \| \vec{y} \|}$$
2. *Tanimoto Coefficient* (Extended jaccard coefficient): $$S(\vec{x}, \vec{y}) = \frac {\vec{x} \cdot \vec{y}}{\| \vec{x} \|^2 +  \| \vec{y} \|^2 - \vec{x} \cdot \vec{y}}$$
- Result is from 0 to 1. 0 -> nothing is shared. 1 -> items are identical

> [!note]
>  While **Mahalanobis distance** is excellent for handling correlated data, it requires calculating the inverse of the covariance matrix, which can be computationally expensive if you have a massive number of attributes ($p$).

