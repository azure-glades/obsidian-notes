
## Problem
Predict whether a fruit is an **Apple** or **Orange** based on its **Weight** (grams).

**Training Data:**

| Fruit  | Weight |
|--------|--------|
| Apple  | 150    |
| Apple  | 155    |
| Apple  | 160    |
| Apple  | 165    |
| Orange | 170    |
| Orange | 175    |
| Orange | 180    |
| Orange | 185    |



## Step 1: Calculate Prior Probabilities
- **P(Apple)** = 4/8 = 0.5
- **P(Orange)** = 4/8 = 0.5



## Step 2: Calculate Likelihoods Using Gaussian Distribution

For continuous variables, we assume the feature follows a **Gaussian (normal) distribution**:
$$
P(x|Class) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left(-\frac{(x - \mu)^2}{2\sigma^2}\right)
$$

Where:
- \(\mu\) = mean of feature for that class
- \(\sigma\) = standard deviation of feature for that class

### For Class = **Apple**:
- Mean (\(\mu_{Apple}\)) = (150+155+160+165)/4 = **162.5**
- Standard deviation (\(\sigma_{Apple}\)) = 5.59 (calculated from variance)

### For Class = **Orange**:
- Mean (\(\mu_{Orange}\)) = (170+175+180+185)/4 = **177.5**
- Standard deviation (\(\sigma_{Orange}\)) = 5.59 (same as Apple by coincidence)


## Step 3: Predict for New Instance
**New fruit:** Weight = **168 grams**

### Calculate P(Apple | Weight=168):
1. **Likelihood**: \(P(Weight=168 | Apple)\)
$$
P(168|Apple) = \frac{1}{\sqrt{2\pi(5.59^2)}} \exp\left(-\frac{(168 - 162.5)^2}{2 \times (5.59)^2}\right)

= \frac{1}{\sqrt{2\pi \times 31.25}} \exp\left(-\frac{(5.5)^2}{2 \times 31.25}\right)

= \frac{1}{14.05} \exp\left(-\frac{30.25}{62.5}\right)

= 0.0712 \times \exp(-0.484)

= 0.0712 \times 0.616 = 0.0439
$$

2. **Posterior (unnormalized)**:
$$
P(Apple|168) \propto P(168|Apple) \times P(Apple) = 0.0439 \times 0.5 = 0.02195
$$

### Calculate P(Orange | Weight=168):
1. **Likelihood**: \(P(Weight=168 | Orange)\)
$$
P(168|Orange) = \frac{1}{\sqrt{2\pi(5.59^2)}} \exp\left(-\frac{(168 - 177.5)^2}{2 \times (5.59)^2}\right)

= \frac{1}{14.05} \exp\left(-\frac{(-9.5)^2}{62.5}\right)

= 0.0712 \times \exp\left(-\frac{90.25}{62.5}\right)

= 0.0712 \times \exp(-1.444)

= 0.0712 \times 0.236 = 0.0168
$$

2. **Posterior (unnormalized)**:
$$
P(Orange|168) \propto P(168|Orange) \times P(Orange) = 0.0168 \times 0.5 = 0.0084
$$



## Step 4: Normalize to Get Actual Probabilities
**Total** = 0.02195 + 0.0084 = 0.03035

- **P(Apple|168)** = 0.02195 / 0.03035 ≈ **0.723 (72.3%)**
- **P(Orange|168)** = 0.0084 / 0.03035 ≈ **0.277 (27.7%)**



## Step 5: Final Prediction
**Prediction: Apple** (72.3% probability)



## Visualization (Conceptual):
```
Apple distribution (mean=162.5)           Orange distribution (mean=177.5)
       ___                                     ___
      /   \                                   /   \
     /     \                                 /     \
____/       \_______               ________/       \_______
150        168      185         150        168      185

Test point (168) is closer to Apple mean → Higher probability of being Apple
```

## Key Points:
1. **Continuous variables** require assuming a probability distribution (Gaussian is most common)
2. The likelihood \(P(x|Class)\) is now a **probability density**, not a count-based probability
3. The prediction depends on how far the test point is from each class mean, scaled by the variance
4. The decision boundary in this case would be at approximately **167.5 grams** (midpoint between 162.5 and 177.5)