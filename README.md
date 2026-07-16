# Telecom Customer Churn Prediction

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=for-the-badge&logo=python)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-ML-orange?style=for-the-badge&logo=scikitlearn)
![TensorFlow](https://img.shields.io/badge/TensorFlow-Neural%20Network-FF6F00?style=for-the-badge&logo=tensorflow)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)


A machine learning project for predicting **telecom customer churn** using classical models and a tuned neural network, with preprocessing, SMOTE, cross-validation, and comparative evaluation on structured customer data.

---

## Project Highlights

- Built an end-to-end workflow for **telecom churn prediction**
- Compared **5 models**:
  - Logistic Regression
  - K-Nearest Neighbours
  - Random Forest
  - Gradient Boosting
  - Neural Network
- Applied **model-specific preprocessing**
- Handled class imbalance using **SMOTE**
- Used **Stratified K-Fold Cross-Validation** for reliable tuning
- Compared models using **Accuracy, Precision, Recall, F1-score, and ROC-AUC**
- Found that **Gradient Boosting** gave the strongest overall discrimination, while the **Neural Network** achieved the best F1-score

---

## Project Overview

Customer churn prediction is an important problem in the telecom industry because losing existing customers directly affects retention and revenue. This project explores how machine learning can be used to identify customers who are likely to churn based on customer profile, service usage, contract type, and billing information.

The main goal was not only to build predictive models, but also to compare them fairly under a consistent workflow and understand which one is most suitable for structured telecom data.

---

## Dataset

- **Dataset:** Telecom Customer Churn Prediction
- **Source:** Maven Analytics dataset on Kaggle
- **Link:** [View Dataset on Kaggle](https://www.kaggle.com/datasets/shilongzhuang/telecom-customer-churn-by-maven-analytics/data)

### Target Preparation
The original dataset contained a `Customer Status` column with:
- `Stayed`
- `Churned`
- `Joined`

For this project:
- `Stayed` was mapped to **0**
- `Churned` was mapped to **1**
- `Joined` records were removed from modelling

---

## Workflow

The project followed this workflow:

1. Data loading and inspection  
2. Target preparation and leakage removal  
3. Missing value handling  
4. Exploratory data analysis  
5. Train-test split with stratification  
6. Model-specific preprocessing  
7. SMOTE on training data only  
8. Hyperparameter tuning  
9. Model evaluation  
10. Final comparison and interpretation  

---

## Models Used

### Classical Machine Learning Models
- Logistic Regression
- K-Nearest Neighbours
- Random Forest
- Gradient Boosting

### Neural Network
- Fully connected feedforward neural network
- Tuned using hidden layer size, dropout, and batch size

---

## Preprocessing Strategy

Different models required different preprocessing pipelines:

| Model | Preprocessing |
|------|---------------|
| Logistic Regression | StandardScaler + OneHotEncoder |
| K-Nearest Neighbours | MinMaxScaler + OneHotEncoder |
| Random Forest | OneHotEncoder + numerical passthrough |
| Gradient Boosting | OneHotEncoder + numerical passthrough |
| Neural Network | MinMaxScaler + OneHotEncoder |

---

## Imbalance Handling

The dataset was moderately imbalanced, so **SMOTE** was used to improve learning for the minority class.

- For classical models, SMOTE was included inside the pipeline
- For the Neural Network, SMOTE was applied after preprocessing the training set
- Test data was never oversampled

---

## Hyperparameter Tuning

- Classical models were tuned using **GridSearchCV**
- Validation used **5-fold Stratified K-Fold Cross-Validation**
- The Neural Network was tuned using a compact manual search over:
  - hidden layer sizes
  - dropout rate
  - batch size

---

## Evaluation Metrics

The models were evaluated using:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC

These metrics were used because churn prediction is an imbalanced classification problem, and accuracy alone does not give a complete picture.

---

## Final Results

| Model | Precision | Recall | F1-score | Accuracy | ROC-AUC |
|------|----------:|-------:|---------:|---------:|--------:|
| Logistic Regression | 0.635 | 0.850 | 0.727 | 0.819 | 0.911 |
| K-Nearest Neighbours | 0.561 | 0.853 | 0.677 | 0.769 | 0.870 |
| Random Forest | 0.778 | 0.714 | 0.745 | 0.861 | 0.921 |
| Gradient Boosting | 0.794 | 0.679 | 0.732 | 0.859 | 0.929 |
| Neural Network | 0.734 | 0.759 | 0.746 | 0.854 | 0.916 |

### Key Findings
- **Gradient Boosting** achieved the highest **ROC-AUC**, making it the strongest overall model
- **Neural Network** achieved the highest **F1-score**, showing the best balance between Precision and Recall
- **Logistic Regression** remained useful because of its strong Recall and interpretability
- **KNN** performed weakest overall for this encoded churn dataset

---

## Repository Structure

```text
telecom-churn-prediction/
├── README.md
├── requirements.txt
├── data/
│   ├── telecom_customer_churn.csv
├── notebooks/
│   └── Customer Churn Prediction_Implementation.ipynb
├── reports/
│   ├── figures/
│   └── final_report.pdf
└── assets/
    └── workflow_diagram.png
