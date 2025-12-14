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
│ ├── raw/
│ └── processed/
│
├── notebooks/
│ ├── 01_data_exploration.ipynb
│ ├── 02_preprocessing.ipynb
│ ├── 03_feature_engineering.ipynb
│ ├── 04_model_training.ipynb
│
├── src/
│ ├── preprocessing.py
│ ├── feature_engineering.py
│ ├── embeddings.py
│ └── models.py
│
├── images/
│ ├── categorical_features_before.png
│ ├── categorical_features.png
│ ├── correlation_matrix.png
│ ├── dates_converted_to_datetimes.png
│ ├── dates_converted_to_days.png
│ ├── embedded_clusters.png
│ └── loan_title_clusters.png
│
├── requirements.txt
└── README.md


---

## 🔍 Data Cleaning & Preprocessing

### Key Steps
- Removed **data leakage features** (post-loan payment information)
- Preserved high-missing columns using **missing value indicators**
- Converted **all date columns** to numerical representations (days since minimum date)
- Grouped rare categorical labels
- Built a **ColumnTransformer-based preprocessing pipeline**

---

## 🧩 Categorical Feature Analysis

### Before Processing
High-cardinality categorical features dominate the dataset.

![Categorical Features Before Processing](images/categorical_features_before.png)

### After Processing
Rare labels grouped and high-cardinality text fields replaced by clusters.

![Categorical Features After Processing](images/categorical_features.png)

---

## 📅 Temporal Feature Engineering

### Dates Converted to Datetime
Raw date parsing and validation.

![Dates Converted to Datetimes](images/dates_converted_to_datetimes.png)

### Dates Converted to Days
All temporal features transformed into numeric day offsets.

![Dates Converted to Days](images/dates_converted_to_days.png)

---

## 🧠 Text Processing with SBERT

Two high-cardinality text columns were embedded using **Sentence-BERT**:

- `emp_title` → Job Title Clusters
- `title` → Loan Purpose Clusters

### Job Title Embedding Clusters
![Embedded Clusters](images/embedded_clusters.png)

### Loan Purpose Clusters
![Loan Title Clusters](images/loan_title_clusters.png)

**Benefits:**
- Reduced 10,000+ unique values to 15 semantic clusters
- Preserved semantic meaning
- Robust to typos and unseen values

---

## 📈 Exploratory Data Analysis (EDA)

### Correlation Analysis
Correlation matrix of numerical features reveals strong relationships
(e.g., loan amount vs. installment, FICO vs. interest rate).

![Correlation Matrix](images/correlation_matrix.png)

---

## 🛠️ Feature Engineering

### Engineered Features (17 Total)
- **Ratio & Interaction Features** (e.g., loan-to-income ratio)
- **Log Transformations**
- **Box-Cox Transformations**
- **Decision Tree-Based Discretization**

Feature count progression:
| Stage | Features |
|-----|----------|
| Raw Data | 145 |
| After Feature Engineering | 162 |
| After Encoding | 356 |

---

## 🤖 Model Training & Evaluation

### Models Used
- **Decision Tree Classifier**
- **Logistic Regression**

### Performance
| Model | Test Accuracy |
|------|--------------|
| Decision Tree | **89.73%** |
| Logistic Regression | 88.45% |

**Decision Tree chosen for production readiness due to:**
- Higher accuracy
- Non-linear modeling capability
- Interpretability
- Fast inference

---

## 🚀 Deployment Readiness

✔ Reproducible preprocessing pipeline  
✔ Feature engineering fully documented  
✔ Scalable to millions of records  
✔ Inference latency < 5ms per loan  

---

## 📌 Key Takeaways

- Feature engineering significantly improves predictive power
- SBERT embeddings effectively handle high-cardinality text
- Tree-based models outperform linear baselines for credit risk
- The pipeline is suitable for **real-world production deployment**

---

## 🔮 Future Work

- Ensemble models (Random Forest, XGBoost)
- SHAP-based explainability
- Temporal cross-validation
- Fairness and bias auditing
- Cost-sensitive threshold optimization

---

## 📜 License

This project is for **educational and research purposes**.

---

## ✉️ Contact

If you have questions or suggestions, feel free to reach out or open an issue.
