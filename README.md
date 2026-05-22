# 🚨 Scalable Credit Card Fraud Detection Using PySpark

Distributed machine learning pipeline for fraud detection using PySpark, Spark MLlib, and HDFS, designed for scalable processing of highly imbalanced financial transaction data.

---

# 📌 Project Overview

This project implements a scalable fraud detection pipeline using **Apache Spark (PySpark)** and **Hadoop Distributed File System (HDFS)** to identify fraudulent financial transactions within a highly imbalanced dataset.

The project focuses not only on predictive performance, but also on the practical challenges of building machine learning systems capable of handling large-scale transactional data efficiently in distributed environments.

The workflow demonstrates:
- Distributed data processing
- Scalable machine learning
- Imbalanced classification handling
- Threshold optimisation
- Fraud-focused evaluation strategies
- Production-oriented big data architecture

---

# 🎯 Business Problem

Financial institutions process millions of transactions daily, making fraud detection a significant operational and financial challenge.

Traditional machine learning workflows often struggle with:
- Extremely imbalanced fraud distributions
- Large-scale transaction volumes
- Computational limitations
- High false-positive costs

This project addresses these challenges by combining distributed computing with machine learning models designed for fraud-sensitive prediction.

The objective is to:
- Detect fraudulent transactions effectively
- Minimise missed fraud cases
- Maintain scalability for large datasets
- Support operational fraud monitoring systems

---

# 📂 Dataset

**Source:** Credit Card Fraud Detection Dataset — Kaggle  
Dataset Link: https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud

## Dataset Characteristics
- ~284,807 transactions
- ~492 fraud cases (~0.17%)
- Highly imbalanced classification problem
- PCA-transformed anonymised features (`V1–V28`)
- Additional features:
  - `Time`
  - `Amount`
  - `Class`

---

# 🛠 Technologies Used

## Big Data & Distributed Systems
- Apache Spark
- PySpark
- Hadoop HDFS
- Spark MLlib

## Machine Learning & Analytics
- Logistic Regression
- Random Forest
- Gradient Boosted Trees (GBT)
- CrossValidator
- ParamGridBuilder

## Data Processing
- Pandas
- NumPy

---

# 🧹 Data Engineering & Preprocessing

The pipeline includes:
- Distributed dataset loading from HDFS
- Missing value inspection
- Feature engineering:
  - Log transformation of transaction amount
  - Extraction of transaction hour from timestamp
- Feature vector construction using `VectorAssembler`
- Standard scaling for Logistic Regression
- Stratified train–test splitting
- Class imbalance handling using weighted learning

---

# 🤖 Machine Learning Models

The following models were trained and evaluated using Spark MLlib:

| Model | Purpose |
|---|---|
| Logistic Regression | Interpretable baseline model |
| Random Forest | Ensemble learning for non-linear fraud patterns |
| Gradient Boosted Trees | Boosted ensemble optimisation |

## Additional Techniques
- Hyperparameter tuning
- Cross-validation
- Threshold optimisation
- Fraud-specific metric evaluation

---

# 📈 Evaluation Strategy

Because fraud detection is highly imbalanced, accuracy alone was not considered reliable.

Instead, evaluation focused on:

- **PR-AUC (Primary Metric)**  
- ROC-AUC  
- Precision  
- Recall  
- F1-score  
- Fraud Precision  
- Fraud Recall  
- Fraud F1-score  

Fraud-specific confusion matrix metrics were also computed:
- True Positives (TP)
- False Positives (FP)
- False Negatives (FN)
- True Negatives (TN)

This evaluation strategy better reflects real-world fraud detection trade-offs.

---

# 🏆 Key Results

## Key Findings
- Ensemble models significantly outperformed baseline Logistic Regression
- Random Forest produced the strongest overall fraud detection performance
- Threshold tuning improved fraud recall but increased false positives
- PR-AUC proved more informative than accuracy in imbalanced settings
- Feature scaling improved Logistic Regression performance
- Distributed Spark workflows enabled scalable processing efficiency

---

# 🔍 Feature Insights

Important fraud-related signals included:
- Transaction amount behaviour
- Temporal transaction patterns
- PCA-derived transactional relationships

Feature importance analysis and Logistic Regression coefficient analysis were exported for interpretability.

---

# ⚡ Scalability & Distributed Architecture

This project was designed with scalability in mind.

## Distributed Components
- **HDFS** for distributed data storage
- **Spark** for parallel data processing
- **Spark MLlib** for scalable machine learning

This architecture enables the pipeline to scale beyond local-memory limitations and better reflects enterprise-level financial analytics systems.

---

# 📁 Project Structure

```bash
fraud_detection_project/

├── fraud_detection_pyspark.ipynb
├── README.md
├── fraud_model_comparison.csv
├── rf_feature_importance.csv
├── lr_coefficients.csv
├── component1_report.pdf
├── component2_report.pdf
└── component3_report.pdf
```

---

# ▶️ Running the Project

## Upload Dataset to HDFS

```bash
hdfs dfs -mkdir -p /user/jadju001/fraud_detection

hdfs dfs -put creditcard.csv /user/jadju001/fraud_detection/
```

## Verify Upload

```bash
hdfs dfs -ls /user/jadju001/fraud_detection/
```

## Execute the Pipeline

```bash
spark-submit fraud_detection_pyspark.py
```

The notebook can also be executed within a configured JupyterHub PySpark environment.

---

# 📤 Outputs

## HDFS Outputs
Predictions saved to:

```bash
hdfs:///user/jadju001/fraud_detection/output/
```

## Generated Files
- `fraud_model_comparison.csv`
- `rf_feature_importance.csv`
- `lr_coefficients.csv`

---

# ⚠️ Limitations

- Severe class imbalance remains challenging
- Threshold tuning introduces operational trade-offs
- Dataset anonymisation limits feature interpretability
- Real-time streaming fraud detection was not implemented

---

# 🚀 Future Improvements

Potential extensions include:
- Real-time fraud detection with Spark Streaming
- SMOTE or advanced imbalance techniques
- Cost-sensitive learning
- Explainable AI integration (SHAP/LIME)
- Deployment using cloud-based distributed environments

---

# 🧠 Business Impact

This project demonstrates how distributed machine learning systems can support:
- Fraud risk reduction
- Operational efficiency
- Scalable financial analytics
- Decision-support systems for financial institutions

It also highlights the importance of aligning machine learning evaluation with real-world fraud costs rather than relying on accuracy alone.

---

# 👤 Author

**Uvietobore Joshua Adjugah**  
MSc Data Science & Artificial Intelligence  
Goldsmiths, University of London  
London, UK
