In machine learning, there are **parameters** and **hyperparameters**:
- **Parameters:** Learned by the model automatically (e.g., weights in a neural network).
- **Hyperparameters:** Set by **you** (the human) before training starts. They control _how_ the model learns.

Think of it like a car: The **parameters** are how the engine internalizes fuel and air to move (the car handles this), while the **hyperparameters** are the settings you choose, like "Sport Mode" or "Eco Mode," which change how the car behaves.

|**Model**|**Common Hyperparameters**|
|---|---|
|**Neural Networks**|**Learning Rate** (how fast it learns), **Number of Layers**, **Batch Size**|
|**Decision Trees**|**Max Depth** (how deep the tree grows), **Minimum samples per leaf**|
|**K-Nearest Neighbors**|**K** (the number of neighbors to look at)|
|**Random Forest**|**Number of Trees** in the forest, **Feature subset size**|
|**Support Vector Machines**|**C** (regularization), **Kernel Type** (Linear, RBF, Poly)|
