# Generalization
**Generalization** = Model’s ability to perform well on **new, unseen data** drawn from the same underlying distribution.
> The gap between training and testing error
- A model that memorizes training data (**overfits**) has **poor generalization**.
- Evaluation methods aim to **approximate** generalization error.
- Simpler models generalize better
Many ways to improve generalization, like [[Regularization]] and dropout methods

Generalization is measured by calculating *generalization error* using [[Cross-validation]] techniques

## Dropout (Deep Learning)
In neural networks, **Dropout** randomly "turns off" a percentage of neurons during each training step. This prevents neurons from becoming overly dependent on each other and forces the network to learn more robust features.