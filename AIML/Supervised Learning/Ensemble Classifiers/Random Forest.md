**Core Concept:** An ensemble learning method that operates by constructing a multitude of decision trees at training time.

**Base Classifier:** Unpruned decision trees (grown to maximum depth).

## Learning Algorithm
1.  **Bootstrap Sampling (Bagging):**
    *   Create multiple bootstrap samples from the original dataset.
    *   Train a separate decision tree on each of these samples.
2.  **Random Feature Selection (Random Subspace Method):**
    *   When splitting at each node of a decision tree, **do not consider all features**.
    *   Instead, take a random sample of features (ignoring some features).
    *   Find the best split only among this random subset.
    *   *Purpose:* This introduces additional randomness to the decision trees and helps avoid overfitting.
3.  **Prediction (Aggregation):**
    *   **Classification:** Use **majority voting** (mode) of the predictions from all the individual trees.
    *   **Regression:** Use the average of the predictions from all the individual trees.

## Advantages & Characteristics
- Less training time
- High accuracy even in large datasets
- Can handle missing or noisy data

*   **Reduces Overfitting:** By averaging multiple deep trees (which usually overfit) and introducing randomness in features, the model is more robust than a single decision tree.
*   **Handles High Dimensionality:** Works well with datasets that have many features because it selects subsets of features at each split.
*   **Importance:** Provides a measure of feature importance based on how much they decrease impurity across the trees.

## Weakness
- Tendency to overfit for regression problems
- Cannot go beyond the range of the dataset when it comes to regression
- Huge memory since there are a lot of decision trees
- Blackbox models

> Related: [[Decision Trees]], [[Bagging]]