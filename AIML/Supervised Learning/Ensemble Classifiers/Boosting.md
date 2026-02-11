Applies weights to datasets and base classifiers to make certain datapoints and classifiers more important. 

data points that are commonly miss classified get higher weight during training
base classifiers that do very well get higher weight during training

this helps improve the accuracy of the base classifier, hence the ensemble is also better.
Boosting reduces the bias of the ensemble classifier

# AdaBoost
Adaptive boosting
error rate of base classifier: formula
importance of classifier: formula
weight update: formula
classification: formula

![[Pasted image 20260131082519.png]]

# Gradient Boosting
Predictive model that has a differentiable loss function.
Instead of updating weights by iteration, you optimize the weights using gradient descent. Exz: XGBoost