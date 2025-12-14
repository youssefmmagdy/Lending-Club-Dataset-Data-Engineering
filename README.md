# Lending Club Data Engineering & Loan Status Prediction

## 📌 Project Overview

This repository contains an **end-to-end data engineering and machine learning pipeline**
for predicting **loan default status** using historical **LendingClub loan data (2007–2018)**.

The project covers:
- Large-scale data ingestion and cleaning
- Advanced feature engineering
- High-cardinality text processing using **SBERT embeddings**
- Exploratory Data Analysis (EDA)
- Machine learning model training and evaluation

The primary goal is to build a **scalable, reproducible, and production-ready pipeline**
for loan risk assessment.

---

## 📊 Dataset Description

- **Source:** LendingClub peer-to-peer lending platform  
- **Time Period:** June 2007 – December 2018  
- **Records:** 2,260,668 loans  
- **Raw Features:** 145  
- **Final Features (after encoding):** 356  

### Target Variable
Binary classification:
- **0 – Good Loan:** Fully Paid, Current, In Grace Period
- **1 – Bad Loan:** Charged Off, Default, Late (16–120 days)

---

## 🏗️ Project Structure

Lending-Club-Data-Engineering/
│
├── data/
│   ├── raw/                 # Original LendingClub CSV files
│   └── processed/           # Cleaned & feature-engineered datasets
│
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_preprocessing.ipynb
│   ├── 03_feature_engineering.ipynb
│   └── 04_model_training.ipynb
│
├── src/
│   ├── preprocessing.py     # Cleaning & leakage prevention
│   ├── feature_engineering.py
│   ├── embeddings.py        # SBERT embeddings & clustering
│   └── models.py            # Model training & evaluation
│
├── images/
│   ├── categorical_features_before.png
│   ├── categorical_features.png
│   ├── dates_converted_to_datetimes.png
│   ├── dates_converted_to_days.png
│   ├── embedded_clusters.png
│   ├── loan_title_clusters.png
│   └── correlation_matrix.png
│
├── requirements.txt
└── README.md

---

## 🔍 Data Cleaning & Preprocessing

### Key Steps
- Removed **data leakage features** (post-loan payment information)
- Preserved high-missing columns using **missing-value indicator flags**
- Converted **all date columns** to numeric representations (days since minimum date)
- Grouped rare categorical labels
- Built a **ColumnTransformer-based preprocessing pipeline**

---

## 🧩 Categorical Feature Analysis

### Before Processing
High-cardinality categorical features dominate the dataset.

<img src="images/categorical_features_before.png" alt="Categorical Features Before Processing" width="100%"/>

---

### After Processing
Rare labels grouped and high-cardinality text fields replaced by semantic clusters.

<img src="images/categorical_features.png" alt="Categorical Features After Processing" width="100%"/>

---

## 📅 Temporal Feature Engineering

### Dates Converted to Datetime
Raw date parsing and validation.

<img src="images/dates_converted_to_datetimes.png" alt="Dates Converted to Datetimes" width="100%"/>

---

### Dates Converted to Days
Dates transformed into numeric offsets for model compatibility.

<img src="images/dates_converted_to_days.png" alt="Dates Converted to Days" width="100%"/>

---

## 🧠 Text Processing with SBERT

Two high-cardinality text columns were embedded using **Sentence-BERT (SBERT)**:

- `emp_title` → Job Title Clusters  
- `title` → Loan Purpose Clusters  

### Job Title Clustering

<img src="images/embedded_clusters.png" alt="Job Title Embedding Clusters" width="100%"/>

---

### Loan Purpose Clustering

<img src="images/loan_title_clusters.png" alt="Loan Purpose Clusters" width="100%"/>

### Benefits
- Reduced 10,000+ unique values → **15 semantic clusters**
- Preserved semantic meaning
- Robust to typos and unseen values
- Significant dimensionality reduction

---

## 📈 Exploratory Data Analysis (EDA)

### Correlation Analysis
Correlation matrix highlights strong relationships between numerical features
(e.g., loan amount vs. installment, FICO vs. interest rate).

<img src="images/correlation_matrix.png" alt="Correlation Matrix" width="100%"/>

---

## 🛠️ Feature Engineering

### Engineered Features (17 Total)
- **Ratio & Interaction Features** (e.g., loan-to-income ratio)
- **Log Transformations**
- **Box-Cox Transformations**
- **Decision Tree–Based Discretization**

### Feature Count Progression

| Stage | Feature Count |
|-----|---------------|
| Raw Data | 145 |
| After Feature Engineering | 162 |
| After Encoding | 356 |

---

## 🤖 Model Training & Evaluation

### Models Implemented
- **Decision Tree Classifier**
- **Logistic Regression**

### Performance Summary

| Model | Test Accuracy |
|-----|---------------|
| Decision Tree | **89.73%** |
| Logistic Regression | 88.45% |

✅ **Decision Tree selected for production** due to:
- Higher accuracy
- Strong non-linear modeling
- Interpretability
- Fast inference

---

## 🚀 Deployment Readiness

✔ Reproducible preprocessing pipeline  
✔ Feature engineering fully documented  
✔ Scales to millions of records  
✔ Inference latency < **5 ms per loan**  

---

## 📌 Key Takeaways

- Feature engineering significantly improves predictive power
- SBERT embeddings effectively handle high-cardinality text
- Tree-based models outperform linear baselines for credit risk
- Pipeline is suitable for **real-world production deployment**

---

## 🔮 Future Work

- Ensemble models (Random Forest, XGBoost)
- SHAP-based explainability
- Temporal cross-validation
- Fairness & bias auditing
- Cost-sensitive threshold optimization

---

## 📜 License

This project is intended for **educational and research purposes**.

---

## ✉️ Contact

Questions, feedback, or contributions are welcome — feel free to open an issue or pull request.
