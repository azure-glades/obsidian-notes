simple classifers make prediction
ensemble uses the majority prediction done by these simple ones

Approach
- train all simple classifiers
- take the predicted class of the simple classifiers
- prediction is the class in majority (conduct majority voting)

Ensemble classifiers have lesser error than their base classifier, since we take majority and it is difficult for a majority of them to make a wrong prediction. error of ensemble = SUM of i from 0 to n/2 {error^i * (1-error)^(n-i)} where error is error of base classifier

base classifiers have to be independent of each other
base classifiers have to be better than random guessing (e > 0.5)

Ensemble methods are best with unstable base classifiers (stuff that is sensitive to data), like unpruned decision tree, ANNs etc
base classifiers have high amount of variance, but less bias. Ensemble classifiers try to reduce variance.

Generating base classifiers:
1. manipulating training set: [[Bagging]], [[Boosting]]
2. manipulating attributes/features: [[Random Forest]]
3. manipulating class labels: Error-correcting output coding
4. manipulating learning algorithm: Injecting randomness into inital weights of neural networks


![[Pasted image 20260131083705.png]]