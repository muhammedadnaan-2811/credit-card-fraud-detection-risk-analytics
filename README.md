# Credit Card Fraud Detection & Risk Analytics

## Project Overview

This project investigates how machine learning can help financial institutions identify fraudulent credit card transactions while balancing fraud detection performance, investigation workload, and potential financial exposure.

Using Python and the Credit Card Fraud Detection dataset, the project develops and compares classification models, optimises fraud detection thresholds, evaluates financial impact, and builds a probability-based risk segmentation framework.

## Business Problem

Credit card fraud detection involves a trade-off between identifying fraudulent transactions and incorrectly flagging legitimate customer activity.

A model that misses fraud may expose a financial institution to potential losses, while a model that flags too many legitimate transactions can increase investigation costs and customer friction.

The objective is to develop a model that supports risk-based decision-making rather than relying solely on classification accuracy.

## Project Objectives

- Analyse patterns in fraudulent and legitimate transactions.
- Perform data quality checks and exploratory data analysis.
- Develop and compare machine learning classification models.
- Evaluate model performance using precision, recall, F1-score, ROC-AUC, and PR-AUC.
- Optimise the classification threshold based on business requirements.
- Estimate detected and missed fraudulent transaction value.
- Conduct cost-sensitive threshold analysis.
- Develop transaction risk segments to support investigation prioritisation.

## Dataset

The project uses the Credit Card Fraud Detection dataset containing anonymised transactions.

The original dataset contains 284,807 transactions and 31 columns, including transaction time, transaction amount, 28 anonymised features (V1–V28), and the fraud indicator (`Class`).

After removing 1,081 duplicate observations, the cleaned dataset contains 283,726 transactions, including 473 fraudulent transactions.

Fraud represents approximately 0.17% of the cleaned dataset, making class imbalance a central modelling challenge.

The raw dataset is not included in this repository.

## Methodology

### 1. Data Quality and Preparation
- Checked missing values and duplicate observations.
- Examined class distribution and transaction amounts.
- Removed exact duplicate observations.
- Created a stratified 80/20 training and test split.

### 2. Exploratory Data Analysis
- Compared transaction amounts across fraud classes.
- Investigated relationships between anonymised features and fraud.
- Examined feature distributions, correlations, and effect sizes.
- Identified patterns that informed subsequent modelling.

### 3. Model Development

The following models were evaluated:

- Logistic Regression
- Class-weighted Logistic Regression
- Random Forest
- XGBoost

### 4. Model Evaluation and Threshold Optimisation

Models were compared using precision, recall, F1-score, ROC-AUC, and PR-AUC.

The XGBoost probability threshold was then evaluated against business-oriented criteria to balance fraud detection and false-positive investigation workload.

### 5. Financial Impact and Risk Segmentation

The analysis estimated fraudulent transaction value identified and missed, evaluated illustrative investigation-cost scenarios, and grouped transactions into probability-based risk bands.

## Key Results

At the default XGBoost threshold of 0.50:

| Metric | Result |
|---|---:|
| Precision | 97.26% |
| Recall | 74.74% |
| F1-score | 84.52% |
| ROC-AUC | 97.85% |
| PR-AUC | 82.84% |

### Selected Operating Threshold: 0.14

A threshold of 0.14 was selected to achieve recall above the default operating point while maintaining precision above 90%.

| Metric | Result |
|---|---:|
| Precision | 90.36% |
| Recall | 78.95% |
| F1-score | 84.27% |
| Fraudulent transactions detected | 75 of 95 |
| False positives | 8 |
| Transactions flagged | 83 |

### Financial Impact

At the selected threshold:

- Fraudulent transaction value identified: €10,965.93
- Fraudulent transaction value missed: €3,800.38
- Total fraudulent transaction value in the test set: €14,766.31
- Monetary recall: 74.26%

The identified transaction value should not be interpreted as confirmed losses prevented. Actual losses depend on factors such as liability, recovery, and chargebacks.

### Risk Segmentation

The High Risk segment contained 83 transactions, of which 75 were fraudulent.

- Observed fraud rate in the High Risk segment: 90.36%
- Share of total fraudulent transaction value identified in this segment: 74.26%

This illustrates the potential value of probability-based prioritisation for fraud investigation teams.

## Business Recommendations

1. **Use multiple evaluation metrics.** Accuracy alone is inadequate for a highly imbalanced fraud dataset.
2. **Select thresholds based on operational objectives.** The appropriate threshold depends on the relative costs of missed fraud and false-positive investigations.
3. **Prioritise high-risk transactions.** Predicted probabilities can help direct investigation resources towards transactions with higher estimated fraud risk.
4. **Measure monetary as well as transaction-level performance.** Transaction recall and monetary recall provide different perspectives on model effectiveness.
5. **Validate cost assumptions.** Real-world implementation requires institution-specific investigation costs, loss estimates, and operational constraints.

## Limitations

- The V1–V28 variables are anonymised PCA components and lack directly interpretable business meanings.
- The dataset is historical and may not represent current fraud patterns.
- Investigation costs are illustrative assumptions rather than institution-specific estimates.
- Missed fraudulent transaction value is a proxy for financial exposure, not confirmed financial loss.
- Threshold selection was conducted using the test-set results, so the reported operating point may be optimistic. A separate validation set should be used for threshold selection in a more rigorous evaluation.
- The project is a research and portfolio prototype, not a production-ready fraud detection system.

## Future Improvements

- Use time-based training, validation, and test splits.
- Perform hyperparameter optimisation and cross-validation.
- Calibrate predicted probabilities.
- Investigate model explainability techniques.
- Evaluate performance under changing fraud patterns.
- Incorporate realistic operational costs and investigation capacity.
- Explore deployment through a transaction-scoring API.

## Tools and Technologies

- Python
- pandas and NumPy
- Matplotlib and Seaborn
- scikit-learn
- XGBoost
- Jupyter Notebook
- Git and GitHub

## Repository Structure

```text
credit-card-fraud-detection-risk-analytics/
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   └── Credit_Card_Fraud_Detection.ipynb
├── figures/
└── data/
    └── README.md
```

## Author

Developed as a portfolio project exploring machine learning, fraud risk analytics, and financial decision-making.
