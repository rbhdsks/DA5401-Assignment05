# DA5401 - Assignment 5

### **Name**: Nitesh Kumar Shah  
### **Roll Number**: ID25M806  

---

## Problem Statement

This assignment explores the challenges of **multi-label classification** in real-world machine learning by using advanced **non-linear dimensionality reduction** techniques like **t-SNE** and **Isomap**.

We will visually analyze the **Yeast dataset** to identify data veracity issues such as:

- Noisy/ambiguous labels  
- Outliers  
- Hard-to-learn data points  

This helps in understanding the difficulties a classifier would face with such complex and imbalanced datasets.

---


---

## Part A: Data Exploration and Baseline Model

### A.1 Data Loading

- Dataset used: **Yeast** from OpenML, provided in ARFF format
- Converted to CSV for easier manipulation
- No missing values found
- The 14 output classes are stored as byte-type values which were converted to integers (0 or 1)

### A.2 Dimensionality Check

- **Features (X)**: 103 gene expression attributes  
- **Labels (Y)**: 14 binary class labels  
- Each data point can belong to multiple classes

### A.3 Label Simplification for Visualization

To simplify the multi-label classification:

- Created four categories:
  1. Most frequent single-label class
  2. Second most frequent single-label class (if any)
  3. Most frequent multi-label combination
  4. Other (everything else)

**Class Imbalance Observed**:

- "Other" category contains nearly 89% of the samples
- Only a single single-label class is significantly present
- Visualization shows a sharp imbalance across categories

### A.4 Feature Scaling

- Standardized features using `StandardScaler`  
- Ensures fair contribution of each feature to distance calculations  
- Required before applying t-SNE or Isomap for meaningful embeddings

---

## Part B: t-SNE and Veracity Inspection

### B.1 t-SNE Implementation and Parameter Tuning

Explored various hyperparameters to evaluate t-SNE performance:

| Parameter           | Tested Values                 | Best Value |
|---------------------|-------------------------------|------------|
| Perplexity          | 5–130                          | 100        |
| Iterations          | 250–1000                       | 800        |
| Learning Rate       | 10–900                         | 300        |
| Early Exaggeration  | 4–96                           | 12         |

- Used **silhouette score** to evaluate cluster separation
- Final embedding showed clean clusters and better category grouping

### B.2 Final t-SNE Visualization

- Used optimal hyperparameters for best visual separation
- Showed some well-defined clusters
- "Other" class dominates and overlaps many clusters
- Visualized final 2D embedding using scatter plots with clear labeling

### B.3 Veracity Inspection

#### Noisy / Ambiguous Labels

- Used a neighborhood-based purity check (7-nearest neighbors)
- Marked samples as ambiguous if most neighbors belong to a different class
- Most ambiguous samples belong to minority classes surrounded by "Other"

#### Outliers

- Detected isolated samples using distance threshold from neighbors
- Points with no close neighbors (95th percentile distance) marked as outliers
- Mostly seen on the cluster fringes, particularly from the "Other" class

#### Hard-to-Learn Regions

- Divided the t-SNE embedding into grid cells
- Highlighted areas with high label diversity (no class > 70%)
- These regions show severe mixing of categories, making classification difficult

---

## Part C: Isomap and Manifold Learning

### C.1–C.2 Isomap Implementation and Visualization

- Used `Isomap` to preserve global data structure (manifold geometry)
- Visualized 2D embedding for various neighbor values (5–15)
- **Best number of neighbors**: 6 (based on silhouette score)

### Distance Matrix Comparison

- Compared pairwise distance matrices:
  - Before (Original High-Dimensional)
  - After t-SNE
  - After Isomap
- t-SNE emphasized local clusters  
- Isomap retained overall geometric structure better

### C.3 Comparison and Manifold Complexity

#### t-SNE vs Isomap

| Technique | Focus        | Strengths                                      |
|-----------|--------------|------------------------------------------------|
| t-SNE     | Local        | Strong visual clusters, good for noise/ambiguity detection |
| Isomap    | Global       | Preserves manifold topology, reveals shape and spread |

#### Data Manifold and Classification Difficulty

- Gene expression data lies on a **highly curved manifold**
- Nonlinear boundaries present
- Simple models struggle in such geometry
- Complex models and manifold-aware methods are required

---

## Summary

This assignment demonstrated the power of visual techniques like t-SNE and Isomap in understanding:

- Label noise  
- Outliers  
- Class imbalance  
- Data manifold structure  

Through parameter tuning and visualization, we explored the **veracity challenges** in multi-label gene expression classification.


---

## Conclusion

Multi-label classification of biological data poses unique challenges due to:

- Overlapping functional categories  
- Noisy or ambiguous labels  
- Highly nonlinear manifolds

This project used **t-SNE** and **Isomap** to inspect and visualize these complexities, enabling better model preparation and interpretation.





