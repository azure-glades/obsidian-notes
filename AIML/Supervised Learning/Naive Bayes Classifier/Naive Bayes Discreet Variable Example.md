## Problem
Predict whether a person will play tennis based on **Outlook**, **Temperature**, **Humidity**, and **Wind**.

**Training Data:**

|Day|Outlook|Temperature|Humidity|Wind|Play?|
|---|---|---|---|---|---|
|1|Sunny|Hot|High|Weak|No|
|2|Sunny|Hot|High|Strong|No|
|3|Overcast|Hot|High|Weak|Yes|
|4|Rain|Mild|High|Weak|Yes|
|5|Rain|Cool|Normal|Weak|Yes|
|6|Rain|Cool|Normal|Strong|No|
|7|Overcast|Cool|Normal|Strong|Yes|
|8|Sunny|Mild|High|Weak|No|
|9|Sunny|Cool|Normal|Weak|Yes|
|10|Rain|Mild|Normal|Weak|Yes|
|11|Sunny|Mild|Normal|Strong|Yes|
|12|Overcast|Mild|High|Strong|Yes|
|13|Overcast|Hot|Normal|Weak|Yes|
|14|Rain|Mild|High|Strong|No|


## Step 1: Calculate Prior Probabilities
From 14 days:
- **P(Yes)** = 9/14 ≈ 0.643  
- **P(No)** = 5/14 ≈ 0.357


## Step 2: Calculate Likelihoods for Each Feature

### For Class = **Yes** (9 instances):

**Outlook:**
- Sunny & Yes: 2/9
- Overcast & Yes: 4/9
- Rain & Yes: 3/9

**Temperature:**
- Hot & Yes: 2/9
- Mild & Yes: 4/9
- Cool & Yes: 3/9

**Humidity:**
- High & Yes: 3/9
- Normal & Yes: 6/9

**Wind:**
- Weak & Yes: 6/9
- Strong & Yes: 3/9

---

### For Class = **No** (5 instances):

**Outlook:**
- Sunny & No: 3/5
- Overcast & No: 0/5
- Rain & No: 2/5

**Temperature:**
- Hot & No: 2/5
- Mild & No: 2/5
- Cool & No: 1/5

**Humidity:**
- High & No: 4/5
- Normal & No: 1/5

**Wind:**
- Weak & No: 2/5
- Strong & No: 3/5


## Step 3: Predict for New Instance
**New day:** (Outlook = Sunny, Temperature = Cool, Humidity = High, Wind = Strong)

### Calculate P(Yes | X):
Using Naive Bayes assumption:
```
P(Yes|X) ∝ P(Sunny|Yes) × P(Cool|Yes) × P(High|Yes) × P(Strong|Yes) × P(Yes)
        = (2/9) × (3/9) × (3/9) × (3/9) × (9/14)
        = 0.222 × 0.333 × 0.333 × 0.333 × 0.643
        = 0.0053
```

### Calculate P(No | X):
```
P(No|X) ∝ P(Sunny|No) × P(Cool|No) × P(High|No) × P(Strong|No) × P(No)
       = (3/5) × (1/5) × (4/5) × (3/5) × (5/14)
       = 0.6 × 0.2 × 0.8 × 0.6 × 0.357
       = 0.0206
```


## Step 4: Normalize to Get Actual Probabilities
**Total** = 0.0053 + 0.0206 = 0.0259

- **P(Yes|X)** = 0.0053 / 0.0259 ≈ **0.205 (20.5%)**
- **P(No|X)** = 0.0206 / 0.0259 ≈ **0.795 (79.5%)**


## Step 5: Final Prediction
**Prediction: No** (do not play tennis) because P(No|X) > P(Yes|X)


## Key Observations from this Example:
1. **Zero probability issue:** Notice `P(Overcast|No) = 0/5 = 0`. If our test instance had Outlook=Overcast, P(No|X) would be 0 regardless of other features. This is why Laplace smoothing is needed in practice.

2. **Naive independence assumption:** We multiply individual probabilities even though features like Humidity and Temperature might be correlated in reality.

3. **Missing features:** If humidity data was missing for our test instance, we would simply omit `P(Humidity|Class)` from the calculation.


