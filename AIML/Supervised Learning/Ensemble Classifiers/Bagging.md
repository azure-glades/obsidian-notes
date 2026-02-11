Bootstrap Aggregating.

Uses bootstrap sampling to make different variations of the data set to train the base classifiers on.
Bootstrap sampling: Sampling with replacement. i.e many samples may have repeated data.
because of bootstrap sampling, around 30% of data is never used (due to sheer probability of never being picked)

Base classifiers are decision stumps

Algorithm:
```al
ALGO Bagging(k - no of bootstrap samples, x - test datapoint)
	FOR (i : 1 -> k)
		> Di = Create a bootstrap sample of size N
		> Train base classifier Ci on bootstrap sample Di
	END-FOR
	C(x) = argmax(Ci(x) = y) //get majority predicted class
RETURN majority class c
```

Bagging reduces the overfitting and high variance (compared to its base classifiers)
