Predicting Overdraft Risk from Personal Transactions

This project predicts whether an account is likely to go into overdraft the following month using historical transactions and budget data. It demonstrates a full end-to-end data science workflow: data cleaning, feature engineering, time-based splitting, model training, evaluation, and interpretation.

📌 Project Overview

Problem: Identify next-month overdraft risk using personal spending behaviour.
Goal: Build a simple but realistic proof-of-concept model for financial risk prediction.
Use Case: Helps users understand spending habits and avoid unnecessary overdraft fees.

Approach:

Clean and standardise raw personal transactions

Merge with budget data

Engineer monthly features

Apply a time-series train/test split

Train a Random Forest classifier

Evaluate performance and interpret results

📂 Data Processing Workflow
Data was dowloaded from Kaggle: https://www.kaggle.com/datasets/bukolafatunde/personal-finance?resource=download

1. Load Data

Imported both datasets (transactions + budget) as pandas DataFrames.

2. Cleaning

Stripped extra spaces from column names

Fixed date formats

Removed duplicates

Normalised category names using a mapping dictionary

3. Merge

Combined transactions and budget data on the cleaned category field.

4. Feature Engineering

Converted dates to monthly periods

Calculated monthly spend per category

Compared each category to its assigned budget

Counted how many categories exceeded the budget

Aggregated monthly totals per account:

total_spent

transactions_count

over_budget_count

Created the target:
next_month_overdraft = total_spent_next_month > 2000

5. One-Hot Encoding

Encoded Account Name as dummy variables.

🤖 Model
Train/Test Split:

Sorted chronologically and used an 80/20 time-series split to avoid data leakage.

Model:

Used a RandomForestClassifier with default settings.

Evaluation:

Generated predictions on the test set and reviewed the classification report.

📊 Results & Analysis

The model achieved 92% accuracy, but the breakdown across classes is more important.

It correctly captured all high-spend (high-risk) months — ideal for overdraft prediction.

Low-spend months were also mostly identified correctly, with only one misclassification.

The model sometimes flags a low-spend month as high-spend, but never misses a genuine high-risk one.

⚠️ Limitations

Very small dataset (only 13 test samples), so metrics aren’t reliable.

Features are simple, and one-hot encoding on limited data can cause overfitting.

The risk label is based on a basic spending threshold — not true banking logic.

Not production-ready (no error handling, no real-time pipeline, minimal feature engineering).

🔧 Future Improvements

Replace the spending threshold with minimum running balance, which is a stronger indicator of overdraft risk.

Introduce model explainability using SHAP or LIME.

Expand dataset or simulate more realistic financial behaviour.