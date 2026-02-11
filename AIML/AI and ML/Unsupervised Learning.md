**Unsupervised Learning** is a branch of machine learning where the model learns from **unlabeled data**.
- **No Labels:** The input data consists of features only, with no pre-defined target or output class (e.g., "cat" vs "dog").
- **Goal:** To model the underlying structure or distribution in the data to learn more about it.
- **Self-Discovery:** The algorithm finds similarities or differences in the data without any explicit guidance.

### Key Tasks in Unsupervised Learning
There are three main types of tasks:
#### 1. [[Clustering]]
The process of grouping a set of objects such that objects in the same group (called a **cluster**) are more similar to each other than to those in other groups.
- **Algorithms:** K-means, Hierarchical Clustering (Agglomerative/Divisive), DBSCAN.
- **Example:** A bank grouping its customers based on spending habits for targeted marketing.
#### 2. Association Rule Learning
Finding interesting relationships or "rules" that describe your data.
- **Algorithms:** Apriori, FP-Growth.
- **Example:** "If a customer buys bread and butter, they are 80% likely to also buy milk." (Market Basket Analysis).
#### 3. Dimensionality Reduction
Reducing the number of random variables under consideration by obtaining a set of principal variables.
- **Algorithms:** Principal Component Analysis (PCA), Singular Value Decomposition (SVD).
- **Example:** Taking a dataset with 100 different features of a house and condensing them into the 3 most important factors to simplify the model.

| **Feature**    | **Supervised Learning**                 | **Unsupervised Learning**                         |
| -------------- | --------------------------------------- | ------------------------------------------------- |
| **Data**       | Labeled (Input + Correct Answer)        | Unlabeled (Input only)                            |
| **Goal**       | Predict a target class or value         | Discover hidden patterns/structure                |
| **Feedback**   | Clear "Right/Wrong" (Error rate)        | No objective "Right" answer (Internal evaluation) |
| **Complexity** | Simple logic, but needs manual labeling | More complex and computationally heavy            |
| **Result**     | Highly accurate predictions             | Descriptive insights (interpretation required)    |
| **Tasks**      | Classification, Regression              | Clustering, Association, Dimensionality Reduction |
### Real-World Applications
- **Customer Segmentation:** Grouping shoppers by behavior to personalize ads.
- **Anomaly Detection:** Identifying "odd" credit card transactions to detect fraud.
- **Social Network Analysis:** Finding communities or "clusters" of friends on platforms like Facebook or LinkedIn.
- **Medical Imaging:** Segmenting different types of tissues in an MRI scan without knowing what they are beforehand.

```mermaid
flowchart LR
    A[Input Data] --> B{Learning Type?}
    
    B -- Supervised --> C[Data is Labeled<br>e.g., Images with tags]
    C --> D[Model Learns Mapping<br>Adjusts to minimize error]
    D --> E[Outcome: Predictive Model<br>Can classify or predict values]
    E --> F[Applications: Spam filters,<br>Medical diagnosis, Price prediction]
    
    B -- Unsupervised --> G[Data is Unlabeled<br>e.g., Raw images or logs]
    G --> H[Model Finds Patterns<br>Clusters or reduces dimensions]
    H --> I[Outcome: Descriptive Insights<br>Structure & groupings revealed]
    I --> J[Applications: Customer segmentation,<br>Anomaly detection, Data compression]
    
    style A fill:#f3f9ff,stroke:#2196f3,color:#0d47a1
    style E fill:#e3f2fd,stroke:#2196f3,color:#0d47a1
    style I fill:#e8f5e9,stroke:#4caf50,color:#1b5e20
    style F fill:#bbdefb,stroke:#2196f3,color:#0d47a1
    style J fill:#c8e6c9,stroke:#4caf50,color:#1b5e20
```

