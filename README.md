# 💧 Water Potability Classification

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Library](https://img.shields.io/badge/Library-Scikit--Learn%20|%20XGBoost%20|%20LightGBM%20|%20Random%20Forest-orange)
![Status](https://img.shields.io/badge/Status-Completed-success)

## 📌 Project Overview
This project focuses on predicting water potability based on chemical properties using advanced Machine Learning techniques. The goal is to classify water samples as **Potable (1)** or **Not Potable (0)**, addressing a critical binary classification problem with significant class imbalance.

This work goes beyond basic model fitting by implementing rigorous **Data Leakage checks** (Label Shuffling, Overlap Controls) to ensure the high performance metrics are genuine and not a result of overfitting or leakage.

##  Dataset Information
The dataset describes water quality metrics including pH, Hardness, Solids, Chloramines, Sulfate, Conductivity, etc.

* **Source:** [Kaggle - Water Potability](https://www.kaggle.com/datasets/developerghost/water-potability)
* ** Important Note on Data Size:** While the standard Kaggle dataset typically contains ~3,000 rows, **this project utilizes an extended dataset of 100,000 records**. This larger volume allows for more reliable statistical analysis and deep learning of complex patterns.
* **Class Imbalance:** The data is heavily imbalanced:
    * `Class 0` (Not Potable): **92.38%**
    * `Class 1` (Potable): **7.62%**

## ⚙️ Methodology & Preprocessing

### 1. Robust Preprocessing
* **Missing Values:** Handled via statistical imputation (Median) to preserve distribution, rather than dropping rows.
* **Outliers:** Managed using clipping strategies, specifically for "Conductivity" which showed a long-tail distribution.
* **Splitting:** Utilized **Stratified Split** to maintain the 92:7 class ratio across Training, Validation, and Test sets.

### 2. Data Leakage Prevention (Sanity Checks)
To validate the surprisingly high accuracy (>99%), extensive sanity checks were performed:
* **Overlap Check:** Confirmed 0% row overlap between Train, Validation, and Test sets.
* **Leakage-Safe Transformation:** All scalers and imputers were fitted **only** on the Training set.
* **Label Shuffle Test:** Randomly shuffled target labels and retrained. The model performance dropped to baseline (Acc ~92%, F1 ~0.0), proving the model is learning real signal, not noise.

##  Model Performance

Several models were trained and compared, including **Logistic Regression (Baseline), XGBoost, LightGBM, and Random Forest**.

### Validation Results (Summary)
| Model | Accuracy | Recall (Class 1) | F1-Score (Class 1) |
| :--- | :---: | :---: | :---: |
| **Random Forest** | **99.73%** | **99.82%** | **98.23%** |
| LightGBM | 99.59% | 99.47% | 97.34% |
| XGBoost | 99.57% | 99.82% | 97.27% |
| Logistic Regression | 78.07% | 84.33% | 36.92% |

###  Final Model: Random Forest
Random Forest was selected as the final model for its superior balance between Precision and Recall on the minority class.

**Final Test Set Metrics:**
* **Accuracy:** 99.81%
* **Recall (Class 1):** 99.91% (Almost no false negatives)
* **F1-Score (Class 1):** 98.75%
* **PR-AUC:** 0.9987

> **Why Random Forest?** It proved robust against noise and effectively captured non-linear relationships in chemical parameters without requiring complex feature engineering, outperforming gradient boosting methods slightly in F1-score for the positive class.

##  Confusion Matrix (Test Set)

*(Ideally, place a screenshot of your confusion matrix here)*

* **False Negatives (FN):** Only **1** potable sample was missed.
* **False Positives (FP):** Only **28** non-potable samples were incorrectly classified.

##  References
1. KL, NR, CB. "Water Quality Index Assessment Using Machine Learning Techniques." *Int. Journal of Env. Science and Development*, 2025.
2. Grinsztajn et al. "Why do tree-based models still outperform deep learning on typical tabular data?" *arXiv*, 2022.

---
**Author:** Yahya Abu Zahra | Computer Engineering Student

**Date:**  January 1, 2026

