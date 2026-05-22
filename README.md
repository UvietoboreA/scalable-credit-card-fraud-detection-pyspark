README.md

# Scalable Credit Card Fraud Detection Using PySpark

## Overview

This project implements a scalable credit card fraud detection system using Apache Spark (PySpark) and Hadoop Distributed File System (HDFS). The goal is to detect fraudulent transactions in a highly imbalanced dataset using distributed machine learning techniques.

The implementation demonstrates how big data technologies can be used to efficiently process and analyse transactional data in a cluster environment, while maintaining scalability for larger datasets.

---

## Dataset

The dataset used is the Credit Card Fraud Detection dataset, available on Kaggle:

https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud

### Dataset Characteristics

- ~284,807 transactions
- ~492 fraud cases (~0.17%)
- Highly imbalanced dataset
- 28 anonymised features (V1–V28 from PCA)
- Additional features: Time, Amount, Class

---

## Technologies Used

- Hadoop HDFS (distributed storage)
- Apache Spark (distributed processing)
- PySpark (implementation)
- Spark MLlib (machine learning models)
- Spark ML tuning tools (CrossValidator and ParamGridBuilder)
- Pandas (results summarisation)

---

## Project Structure

fraud_detection_project/

├── fraud_detection_pyspark.ipynb
├── README.md
├── fraud_model_comparison.csv
├── rf_feature_importance.csv
├── lr_coefficients.csv
└── component1_report.pdf
└── component2_report.pdf
└── component3_report.pdf

---

## Data Storage (HDFS)

The dataset is stored in HDFS at:

hdfs:///user/jadju001/fraud_detection/creditcard.csv

### Uploading Dataset to HDFS

hdfs dfs -mkdir -p /user/jadju001/fraud_detection
hdfs dfs -put creditcard.csv /user/jadju001/fraud_detection/

### Verify Upload

hdfs dfs -ls /user/jadju001/fraud_detection/

---

## How to Run the Project

1. Ensure Spark is available on the university cluster environment.

2. Execute the script:

spark-submit fraud_detection_pyspark.py

The code may also be run in a JupyterHub environment configured with PySpark.

---

## Optional: Run on Smaller Subset

If execution time is high, modify the data loading step:

df = spark.read.csv(...).limit(50000)

This allows the examiners to test the pipeline more quickly while preserving the structure of the workflow.

---

## Implementation Workflow

The project follows a structured pipeline:

1. Load the dataset from HDFS into a Spark DataFrame
2. Perform data inspection and missing value checks
3. Conduct exploratory data analysis
4. Apply feature engineering:
   - Log transformation of Amount
   - Extraction of Hour from Time
5. Prepare features using VectorAssembler
6. Apply StandardScaler for Logistic Regression only
7. Split data into training and testing sets
8. Handle class imbalance using class weighting
9. Train machine learning models:
   - Logistic Regression (scaled features)
   - Random Forest (unscaled features)
   - Gradient Boosted Trees (unscaled features)
10. Apply hyperparameter tuning and cross-validation to Random Forest
11. Evaluate models using:
   - ROC-AUC
   - PR-AUC
   - F1-score
   - Precision and Recall
12. Compute fraud-specific metrics:
   - True Positives (TP), False Positives (FP)
   - False Negatives (FN), True Negatives (TN)
   - Fraud Precision, Fraud Recall, Fraud F1
13. Perform threshold tuning for Logistic Regression
14. Analyse feature importance
15. Save predictions and summary outputs

---

## Outputs

### HDFS Outputs

Predictions are saved to:

hdfs:///user/jadju001/fraud_detection/output/

Includes:
- Logistic Regression predictions
- Random Forest predictions
- Gradient Boosted Trees predictions
- Threshold-tuned Logistic Regression predictions

### Local Outputs (Cluster)

- fraud_model_comparison.csv
- rf_feature_importance.csv
- lr_coefficients.csv

---

## Key Insights

- Fraud detection is a highly imbalanced classification problem
- PR-AUC and fraud-specific metrics are more meaningful than accuracy
- Ensemble models outperform Logistic Regression for fraud detection
- Threshold tuning increases fraud recall but significantly increases false positives
- Feature scaling improves Logistic Regression preprocessing
- Cross-validation and hyperparameter tuning improve the robustness of Random Forest
- Spark enables scalable processing for large datasets

---

## Scalability

The project uses:

- HDFS for distributed data storage
- Spark for parallel data processing

This architecture allows the pipeline to scale to significantly larger datasets, making it suitable for real-world financial systems.

---

## Reproducibility

To reproduce the results:

1. Upload the dataset to HDFS
2. Run the PySpark script
3. Ensure the Spark environment is configured correctly

All steps from data loading to model evaluation are included in the script.

---

## Author

Uvietobore Joshua Adjugah
MSc Data Science & Artificial Intelligence FT

---

## Notes

- Ensure the dataset is uploaded to HDFS before running
- Update HDFS paths if using a different username
- Results are reproducible using the provided script
