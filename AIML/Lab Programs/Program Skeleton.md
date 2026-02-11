Programs are always

```python
# ...
import packages
# ...

# import data
load data from path/csv/load_iris

# scale and split data
StandardScaler().transform()
X_train, X_test, y_train, y_test = train_test_split(data)

# core algo
def Learning algorithm
	intialize algorithm states ...

	while not Converged:
		# core computation
		calculate values/gradient/etc ...
	
		# update states
		update states/weights/probabilities ...
	return model/states/weights

# helper funcs

# initialize model
model = LearningAlgorithm()

# train model
model.train()

# test model
model.test()
```


An invariant = what MUST stay true after every iteration.


# K means clustering
Invariant:
- k is the number of classes we make
- Each point belongs to 1 cluster.
- Centroid -> mean of assigned points in a cluster

Algo
```al

// TRAINING

> select k random initial centroids
WHILE (centroids change OR reach max iterations)
	assign points to closest centroids
	calculate mean of each cluster
	assign centroids := mean
END-WHILE

// TESTING point p

calculate distance from p to each centroid
SORT(distances)
predict := class of closest centroid to p
```

# K Nearest Neighbhours
Invariant:
- dataset doesnt change
- majority vote is used to predict point

Algo
```al
// No TRAINING

// TESTING

FOR ALL test points
	FOR ALL training points
		calculate distance from training point to test point
	END-FOR
	SORT(distances)
	set of closest k points := SELECT(k nearest points FROM distances)
	predict := ARGMAX(class of point IN set of closest k points)
END-FOR
```


# Naive Bayes Classifier
Invariant:
- calculate Priors and likelihoods
- highest probability class is the prediction

Algo
```
// TRAINING
FOR EACH y IN classes
	calculate Priors
	FOR EACH x in Features
		calculate Likelihood[y][x]

// TESTING on X
FOR EACH y IN classes
	calculate Posteriors

predict := class of MAX(Posterior)
```

# Logistic Regression
Invariant:
- learning rate
- sigmoid
- always do gradient descent

Algo
``` al
// TRAINING

> initialize weights w, bias b
// w, b are vectors whos lengths are equal to no. of features

FOR n iterations
	FOR EACH sample x IN dataset
		z = w*x + b
		
		y_hat = sigmoid(z)           // y_hat is also a vector [y1 y2 y3 ...]
		error = y_hat - y            // y is actual values for x
		w,b := update(w, b)

FUNC sigmoid(z)
	RETURN 1/(1 + exp(-z))

FUNC update(w, b)
	w = w + learning_rate * error * x
	b = b + learning_rate * error
RETURN w, b

// TESTING x'

prediction := w*x' + b
// w and b are the weights and bias after training
```

# Hill climb search
Invariant, we always do this:
- Check neighbhours of current state
- go to best neighbhour

Algo
```al
current = initial

WHILE TRUE
	generate neighbhour from current
	best = MAX(neighbhour)
	IF best <= current
		BREAK
	current = best
```

# 8 Puzzle using A star
Invariant:
- State = board configuration
- f, g and h
- always expand lowest f
- stop when goal is reached

Algo
```al

open = [ (start, 0) ]
closed = []

WHILE open NOT EMPTY
	current := get node in open with lowest f(n) value
	IF current == goal
		BREAK
	
	move current from open to closed
	FOR EACH neighbhour OF current
		IF neighbhour IN closed
			CONTINUE
		compute g, h, f of neighbhour
		add (neighbhour, f(neighbhour)) to open

```

# Alpha Beta pruning

```al

ALGORITHM minimax(depth, node_index, isMax, values, alpha, beta)
	IF (depth == 3)
		RETURN values[node_index]
	
	IF isMax
		best = -infinity
		FOR i IN {0,1}
			val = minimax(depth+1, 2*node_index + i, False, values, alpha, beta)
			best = MAX(val, best)
			alpha = MAX(alpha, best)
			IF alpha >= beta
				BREAK
		RETURN best
	ELSE
		best = infinity
		FOR i in {0, 1}
			val = minimax(depth+1, 2*node_index + i, True, values, alpha, beta)
			best = MIN(val, best)
			beta = MIN(beta, best)
			IF alpha >= beta
				BREAK
		RETURN best
```

