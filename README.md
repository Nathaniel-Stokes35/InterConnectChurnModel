# Discovering InterConnect Churn

This project investigates customer churn at InterConnect using customer, contract, internet, and phone data. It leverages Python, data preprocessing, exploratory data analysis, and machine learning (XGBoost) to identify customers most at risk of leaving the service.

## 📁 Project Structure

datasets 
<ul>
  <li>contract.csv</li>
  <li>internet.csv</li>
  <li>personal.csv</li>
  <li>phone.csv</li>
</ul>
InterConnectChurn.ipynb

## 🚀 Purpose

Customer churn directly affects business profitability. This project aims to:

- Understand which features contribute most to churn.
- Predict which customers are at risk.
- Segment customers into churn risk tiers to guide retention strategies.

## 🧩 Data Sources

Four CSV files found in the `datasets` folder:

- **contract.csv** – Subscription details and contract types.
- **internet.csv** – Internet service details per customer.
- **personal.csv** – Demographic and personal data.
- **phone.csv** – Phone service information.

## 🔍 Exploratory Data Analysis

Each dataset was inspected for:

- Shape and consistency
- Missing values
- Redundancy or duplicate records

Key findings:
- Datasets are mostly aligned on `customerID`.
- No major missing values.
- Phone and internet data were combined into a unified `product_df`.
- Contract and personal data were merged into `client_df`.

## 🧼 Preprocessing Highlights

- Removed duplicate entries by `customerID`.
- Converted data types (e.g., dates, numeric fields).
- Extracted year and month from start dates.
- Created `is_active` target label based on absence of `EndDate`.
- Categorical variables one-hot encoded.
- Applied a logarithmic transformation to `TotalCharges` due to skew.

## 📊 Visualization Insights

- Histograms and box plots revealed right-skew in `TotalCharges`.
- Most customers joined in 2019, with fewer in early 2020 implying record capture date at the end of first quarter 2020.
- These trends were used to design model features.

## 🤖 Modeling Strategy

- **Model Used**: XGBoost Classifier
- **Target Variable**: `is_active` (1 if still active, 0 if churned)
- **Train/Val/Test Split**: 57% / 20% / 17.65%
- **Feature Selection**: Included all numeric and encoded categorical variables
- **Hyperparameter Tuning**: Performed via RandomizedSearchCV
- **Interpretability**: SHAP values used to visualize feature importance and contribution to predictions.

## 🎯 Risk Classification Plan

Customers will be segmented into:

- **Very Small Risk**
- **Small Risk**
- **Moderate Risk**
- **High Risk**
- **Very High Risk**

This supports targeted marketing strategies.

## ❓ Unanswered Questions

1. **Snapshot Date Accuracy**: Data cutoff assumed to be March 1, 2020. Final confirmation needed.
2. **Definition of `TotalCharges`**: Clarify whether it reflects historical charges only or includes future estimates (to prevent data leakage).

## 🛠 Dependencies

All packages will auto-install if missing:

```bash
pandas
numpy
matplotlib
seaborn
scikit-learn
xgboost
shap
```
