Task: Classify a data point
Performance Measure: Classification accuracy
Experience: Dataset is supervised data

[[Class notes on decision trees]]
[[Pruning Techniques]]

Decision trees are basically a set of questions that let you decide on the class of a data point
A tree whos internal nodes are decision nodes (i.e a question) and leaf nodes are pure classes.
We split the dataset at each node based on a chosen feature. Deciding the best feature to split from is done by comparing the purity of the resulting nodes when we split with each feature. See [[Impurity Measures]]
The higher the node in the tree, the more decisive (important) the feature is.

Approach: See [[Decision Tree Induction Algorithms]]
1. Start with full dataset
2. For all features, evaluate the purity of the nodes when you split on that feature
3. Find the feature that causes the biggest improvement in purity
4. Split based on that feature. Now for further splitting this feature cannot be used
5. Repeat for each child node that is made
6. Stop when a child node is pure (has only 1 class) or stop when we reach a maximum depth (If its still impure, then classify as the most common class in that node). There are other stopping criteria also

| Stopping Criteria      | **Description**                                                                                                                                   |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Pure Node**          | The most natural stop; all instances in the node belong to the same class.                                                                        |
| **No Attributes Left** | There are no more features left to split on (common in small datasets).                                                                           |
| **Min Samples Leaf**   | A split is only allowed if it results in leaf nodes that contain at least $n$ samples. This prevents the tree from creating rules for "outliers." |
| **Maximum Depth**      | Limits how many "levels" the tree can grow (e.g., a `max_depth` of 3). This keeps the model simple and generalizable.                             |

## Advantage
- simple and quick to train
- very fast
- easy to interpret (white-box)
- can handle mixed data types or attributes
- can handle redundant attributes
- can handle irrelevant attribues
- can handle outliers easily
- higher nodes have more important attributes, hence more decisive attributes can be found
## Disadvantage
- High tendency to overfit. Large decision trees with big depth end up memorizing the data
- High variance, low bias
- Cannot handle missing attributes
- Interacting attributes can mess up the decsion tree
- Can only split on a single attribute each time
# Splitting a node
Nodes can be split in a number of ways. Depends on the algorithm
1. Binary split: always split into 2 child nodes.
	- if chosen attribute is binary, then it is simple
	- if chosen attribute is continuous, then you divide the values into all possible classes and group those classes into 2s and find the best spot to split those classes.
		- find the best value v where you can do A > v and A <= v split. 
	- if chosen attribute is ordinal or nominal, then you group the classes into 2s and find the best grouping
2. Multi-way split: Split into multiple nodes. Best for nominal/ordinal since each class gets its own node

