# 🧠 End-to-End Machine Learning Pipeline for Diabetes Prediction

## 📌 Overview

This project presents a **fully validated, end-to-end machine learning pipeline** for predicting diabetes using real-world clinical data from the NHANES dataset.

Unlike basic ML projects, this work follows **industry-level best practices**, including:

* Proper **cross-validation**
* Handling of **class imbalance**
* Prevention of **data leakage**
* Use of **appropriate evaluation metrics**
* **Threshold optimization** based on clinical context
* **Model calibration analysis**

The goal is not just to build a model, but to demonstrate how to **develop reliable and interpretable ML systems for healthcare applications**.

---

## 🎯 Research Question

> Can we build a robust and well-validated machine learning model to predict diabetes status from clinical variables, using evaluation strategies appropriate for imbalanced medical data?

---

## 📊 Dataset

* Source: NHANES (National Health and Nutrition Examination Survey)
* Size: 4,515 patients, 10 variables
* Type: Real-world clinical data
* Features include:
  * Demographics (Age, Gender, Race)
  * Clinical measurements (BMI, Blood Pressure, Cholesterol)
  * Lifestyle variables (Physical activity, Sleep)

⚠️ Note: The dataset is **imbalanced** (89.5% No diabetes vs 10.5% Yes), reflecting real clinical scenarios.

---

## 🏗️ Pipeline Architecture

### 1. Data Preparation
* Feature selection based on clinical relevance
* Removal of missing values (complete case analysis)
* Deduplication

### 2. Train/Test Split
* Stratified 80/20 split to preserve class distribution

### 3. Preprocessing Pipeline
* Centering and scaling fitted **only on training data**
* Prevents **data leakage**

### 4. Handling Class Imbalance
* SMOTE applied **inside each CV fold**
* Ensures realistic evaluation

### 5. Model Training
* Algorithm: Random Forest
* Hyperparameter tuning: mtry ∈ {2, 3, 4, 5}
* Optimal: **mtry = 3**

### 6. Validation Strategy
* **10-fold cross-validation**
* Final evaluation on held-out test set

---

## 📈 Model Evaluation

| Metric | Cross-Validated | Test Set |
|---|---|---|
| ROC-AUC | 0.813 | 0.788 |
| PR-AUC | — | 0.282 |
| F1 Score | — | 0.385 |
| Sensitivity | 0.923 | 0.442 |
| Specificity | 0.336 | 0.899 |

👉 **Why this matters:**
* ROC-AUC alone is not sufficient for imbalanced datasets
* PR-AUC provides a more realistic view of minority class performance
* F1 balances precision and recall

---

## ⚖️ Threshold Optimization

| Threshold | Use case |
|---|---|
| 0.5 | Optimal for F1 |
| 0.3 | Clinically preferable (screening) |

👉 Lower thresholds increase sensitivity — critical when **missing a positive case is more costly than false positives**.

---

## 📉 Calibration Analysis

* Well calibrated at low-risk ranges (0.0–0.4)
* Less reliable at higher probabilities due to data scarcity
* Can be improved with Platt scaling or isotonic regression

---

## 🧠 Key Takeaways

* Proper validation drastically changes how model performance should be interpreted
* Handling class imbalance is essential in clinical ML
* Evaluation metrics must match the problem (PR-AUC > accuracy)
* Threshold selection should be driven by **real-world cost of errors**
* Calibration matters when probabilities are used for decision-making

---

## ⚠️ Limitations

* Sensitivity remains moderate (~44%) — many positive cases still missed
* Limited feature set (no HbA1c or glucose biomarkers)
* No external validation dataset

---

## 🚀 Future Work

* Compare multiple models (XGBoost, Logistic Regression)
* Explore advanced imbalance techniques (SMOTE variants)
* Improve calibration (Platt scaling / isotonic regression)
* Validate on independent datasets

---

## 🛠️ Tech Stack

* R 4.5.3
* `tidyverse`, `caret`, `randomForest`
* `themis` (SMOTE), `pROC`, `precrec`, `MLmetrics`

## 📁 Files

* `ml_pipeline_diabetes.Rmd` — R Markdown source code
* `ml_pipeline_diabetes.html` — Full rendered report

---

## 👩‍💻 Author

**Noelia Caba Martin**
Junior Data Analyst / Biostatistician
Interested in health data, bioinformatics and applied machine learning

---

⭐ Feel free to star the repo or connect!
