# Fintech Credit Risk Default Prediction (Leakage-Safe)

## 📌 Business Problem
In consumer lending, issuing credit to high-risk borrowers leads to direct financial losses through defaults, while being overly conservative reduces revenue and growth.  
The goal of this project is to predict loan default risk at application time, using only information available before loan approval.

This mirrors real-world fintech credit underwriting systems.

---

## 🎯 Objective
Build a binary classification model to predict whether a loan will be Charged Off (default) or Fully Paid, while strictly preventing data leakage.

---

## 📊 Dataset
- Source: Public lending dataset (loan-level records)
- Size: ~44,000 completed loans
- Target variable:
  - 0 → Fully Paid  
  - 1 → Charged Off  

⚠️ Raw data is intentionally excluded from this repository to follow professional data governance practices.

---

## 🔍 Key Challenges Addressed

### 1️⃣ Data Leakage Prevention
Loan datasets often include post-loan information such as:
- repayment amounts
- recoveries
- last payment dates
- collections and settlements

Using these features would inflate model performance artificially.

✔️ All post-disbursement variables were explicitly identified and removed before modeling.

---

### 2️⃣ Feature Selection Strategy (Production-Safe)
Instead of reacting to errors later, features were selected using:
- Whitelist approach (application-time variables only)
- Hard blocklist for known leakage variables
- Prefix-based filtering (e.g., total_pymnt, recoveries, last_pymnt_*)

This ensures the model is deployable in real production systems.

---

## 🧹 Data Cleaning & Preparation
- Removed columns with 100% missing values
- Dropped high-missing and irrelevant joint-account features
- Median imputation for numeric variables
- Zero-fill for time-since features (mths_since_*)
- One-hot encoding for categorical variables
- Feature scaling using StandardScaler

All preprocessing is implemented using scikit-learn Pipelines to prevent train/test leakage.

---

## 🧠 Model
- Algorithm: Logistic Regression
- Reason:
  - Interpretable
  - Industry-standard baseline in credit risk
  - Suitable for regulated environments

Pipeline structure:
ColumnTransformer → Scaling / Encoding → Logistic Regression

---

## 📈 Model Performance (Test Set)

- ROC-AUC: ~0.73
- Accuracy: ~0.67
- Recall (Defaults): ~0.67

Confusion Matrix:
[[4655 2341]
 [ 600 1205]]

Interpretation:
- Model captures ~67% of defaulters
- Balanced trade-off between risk detection and false positives
- Performance is realistic and not inflated by leakage

---

## 🧠 Why This Project Matters
This project demonstrates:
- Real-world credit risk thinking
- Strong understanding of data leakage
- Production-ready feature engineering
- Business-oriented model evaluation

---

## 📓 Notebook
Main analysis notebook:
notebooks/credit_risk_default_prediction.ipynb

---

## 🛠️ Tech Stack
- Python
- Pandas, NumPy
- Scikit-learn
- Matplotlib
- Jupyter Notebook

---

## 📬 Author
Avinash Anthony  
Junior Data Scientist | Fintech & Risk Analytics
