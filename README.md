# Credit Risk Default Prediction
📓 Main analysis notebook: `notebooks/credit_risk_default_prediction.ipynb`

## Problem Statement
Predict whether a loan will default using only information available at the time of loan approval.

## Key Challenge
The dataset contains post-loan variables such as payments, recoveries, and settlements that cause severe data leakage.
Initial models achieved unrealistically perfect performance, which was treated as a red flag.

## Solution Approach
- Audited features based on causality and timing
- Removed all post-loan and outcome-derived variables
- Enforced a strict approval-time feature whitelist
- Built an interpretable Logistic Regression model

## Model & Evaluation
- Model: Logistic Regression (class_weight='balanced')
- Metrics: ROC-AUC, Recall for defaulters

### Results
- ROC-AUC: ~0.73
- Recall (Default): ~0.67

## Business Insight
The model prioritizes catching defaulters over raw accuracy, aligning with real-world credit risk trade-offs.

## Tools Used
- Python
- Pandas, NumPy
- Scikit-learn
- Matplotlib
