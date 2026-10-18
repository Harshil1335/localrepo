# Leukemia Classification Using Harris Hawks Optimization and KNN

A machine learning project exploring leukemia classification from high-dimensional gene-expression data. It examines conventional feature-selection methods and uses **Harris Hawks Optimization (HHO)** to tune the hyperparameters of a **K-Nearest Neighbors (KNN)** classifier.

> **Project scope:** ANOVA and Recursive Feature Elimination (RFE) are used for feature-selection experiments. In the HHO experiment, HHO optimizes **KNN hyperparameters**, not gene-feature subsets.

## Project overview

Gene-expression datasets can contain thousands of measurements but relatively few samples. This project explores two related questions:

1. How do feature-selection methods such as ANOVA and RFE affect KNN classification?
2. Can HHO search for suitable KNN hyperparameters instead of choosing them manually?

The classification task is to distinguish **leukemia** samples from **healthy** samples in a gene-expression dataset with approximately **22,000 features**.

## Methods

### Feature-selection experiments

- **ANOVA (SelectKBest):** ranks features by their statistical association with the class labels and selects a subset.
- **Recursive Feature Elimination (RFE):** repeatedly removes less-important features based on an estimator.
- **KNN:** evaluates classification using the selected feature sets.

### HHO-based KNN optimization

Harris Hawks Optimization is a population-based optimization algorithm inspired by the cooperative hunting behavior of Harris's hawks. In this project, it is used to search over KNN settings:

| Parameter | Purpose |
| --- | --- |
| `n_neighbors` | Number of neighboring samples used for prediction |
| `p` | Distance parameter for the Minkowski metric |
| `weights` | Uniform or distance-based neighbor voting |

The optimization procedure evaluates candidate parameter settings and searches for a combination that performs well under its evaluation objective.

## Workflow

```text
Gene-expression dataset
        |
        v
Data preparation and label separation
        |
        +------------------------------+
        |                              |
        v                              v
ANOVA / RFE experiments       HHO hyperparameter search
        |                              |
        v                              v
KNN classification             Tuned KNN classifier
        |                              |
        +---------------+--------------+
                        |
                        v
              Classification evaluation
```

These are related experiments, not a single pipeline in which HHO selects genes.

## Technology stack

- Python
- NumPy and pandas
- scikit-learn
- Matplotlib (for notebook visualizations, where used)
- Custom Harris Hawks Optimization implementation
- Jupyter Notebook

## Results and interpretation

The notebook contains experimental classification results for the ANOVA, RFE, and HHO-based KNN approaches. **Do not treat these results as a controlled head-to-head benchmark without further validation**: the experimental settings and data splits are not fully aligned.

For a stronger comparison, use the same train/test partitions, fit preprocessing and feature selection only on training data, and evaluate with stratified cross-validation. Report accuracy alongside a confusion matrix and class-level precision, recall, and F1-score.

## Limitations

- The dataset has many features relative to its sample count, increasing the risk of overfitting.
- Preprocessing and feature selection must be kept within training folds to avoid data leakage.
- Any sample identifier must be excluded from predictive features.
- Reported test accuracy alone does not establish generalization to unseen clinical datasets.
- This is an **educational machine learning experiment**, not a medical diagnostic tool.

## Future improvements

- Use a consistent, leakage-free evaluation pipeline across all approaches.
- Add repeated stratified cross-validation and class-level metrics.
- Compare tuned KNN with baseline KNN under identical conditions.
- Add a reproducible environment file and a documented dataset reference.
- Investigate feature stability and sensitivity to random seeds.

## Author

**Harshil Bhardwaj**  
[GitHub](https://github.com/Harshil1335) | [LinkedIn](https://www.linkedin.com/in/harshil-bhardwaj-581452283)
