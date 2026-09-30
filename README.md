# Evaluating the Effect of LASSO-Based Sparsification on the Consistency and Stability of Explainable Boosting Machines

This repository contains the code and experimental results for the term paper:

> **Evaluating the Effect of LASSO-Based Sparsification on the Consistency and Stability of Explainable Boosting Machines**

**Author:** Niraj Shinde  
**Program:** MSc in Natural Language Processing  
**University of Trier**

---

## Overview

Explainable Boosting Machines (EBMs) are interpretable machine-learning models based on the additive structure of Generalized Additive Models. However, in high-dimensional datasets, an EBM can contain a large number of terms, making the model more difficult to inspect.

Greenwell et al. proposed a LASSO-based post-processing method that sparsifies an already-trained EBM by reweighting its learned term contributions and removing terms whose LASSO coefficients become zero.

This project implements the LASSO-based sparsification approach and extends its evaluation beyond predictive performance. In particular, the study investigates whether the explanatory structure of an EBM is preserved after sparsification.

---

## Research Objective

The main objective of this project is to investigate:

> **How does LASSO-based sparsification affect the predictive performance, explanation consistency, and explanation stability of an Explainable Boosting Machine?**

The evaluation considers three main aspects:

- **Predictive performance** — whether sparsification changes test-set prediction error.
- **Explanation consistency** — whether explanations of the sparse EBM remain similar to those of the original EBM.
- **Explanation stability** — whether explanations remain stable when small perturbations are introduced into the input.

---

## Main Contributions

This project:

1. Implements LASSO-based post-processing for an Explainable Boosting Machine.
2. Evaluates explanation consistency between the original and sparsified EBM.
3. Evaluates explanation stability under small input perturbations.
4. Analyzes the trade-off between model sparsity, predictive performance, and explanation preservation.

---

## Dataset

The experiments use the **ALS dataset** described in Greenwell et al.

The dataset contains:

- 1,822 observations
- 369 predictor variables
- Continuous target variable: `dFRS`
- A predefined `testset` indicator

The non-test observations are divided into training and validation sets, while the predefined test set is kept separate for final evaluation.

---

## Experimental Setup

The original study used 25 inner bags, 25 outer bags, and pairwise interactions.

Due to the computational cost of training EBMs on the high-dimensional ALS dataset, this project uses a reduced configuration:

| Setting | Configuration |
|---|---:|
| Inner bags | 5 |
| Outer bags | 5 |
| Pairwise interactions | Disabled |
| Main-effect terms | 369 |
| Total baseline terms | 369 |

Therefore, this project follows the **LASSO-based sparsification methodology** of Greenwell et al. but does not exactly reproduce their original computational configuration.

---

## Method

The experimental workflow is:

```text
ALS Dataset
     |
     v
Train Baseline EBM
     |
     v
Calculate EBM Term Contributions
     |
     v
Fit Non-Negative LASSO
     |
     v
Select LASSO Regularization Parameter
     |
     v
Reweight EBM Terms
     |
     v
Remove Zero-Coefficient Terms
     |
     v
Evaluate Sparse EBM
