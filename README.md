# 🛒 E-commerce Customer Analytics & Market Basket Analysis

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E)
![mlxtend](https://img.shields.io/badge/mlxtend-Apriori-green)

An end-to-end machine learning project on e-commerce customer data covering **prediction, customer segmentation, and product association mining**. The project includes **Market Basket Analysis using the Apriori algorithm** to discover frequent itemsets and association rules from customer purchases.

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Dataset](#-dataset)
- [Methodology](#-methodology)
- [Results](#-results)
- [Project Structure](#-project-structure)
- [Installation & Usage](#-installation--usage)
- [Tech Stack](#-tech-stack)
- [Key Learnings](#-key-learnings)
- [Future Improvements](#-future-improvements)
- [Author](#-author)

---

## 🎯 Project Overview

This project performs four machine learning tasks on a single e-commerce dataset:

| Task | Goal | Algorithm |
|------|------|-----------|
| **Regression** | Predict customer `SpendingScore` | Linear Regression |
| **Classification** | Predict customer `ChurnStatus` | Random Forest Classifier |
| **Clustering** | Segment customers into groups | K-Means (k = 3) |
| **Association Rules** | Find products frequently bought together | Apriori (mlxtend) |

---

## 📊 Dataset

**File:** `data/ecommerce_multitask_dataset.csv`
**Size:** 1,000 customers

| Column | Description |
|--------|-------------|
| `CustomerID` | Unique customer identifier |
| `Age` | Customer age |
| `AnnualIncome` | Annual income |
| `SpendingScore` | Spending score assigned to the customer |
| `TotalPurchases` | Number of purchases made |
| `ChurnStatus` | 1 = churned, 0 = retained |
| `TotalSpent` | Total amount spent |
| `ItemsBought` | Comma-separated list of products purchased |

**Products in the data include:** Charger, Phone, Laptop, Mouse, Keyboard, Shoes, T-Shirt, Cover, Headphones, Smartwatch.

---

## 🔬 Methodology

### 1. Regression: Spending Score Prediction
- **Features:** `Age`, `AnnualIncome`, `TotalPurchases`, `TotalSpent`
- **Target:** `SpendingScore`
- 80/20 train-test split, evaluated with R² score

### 2. Classification: Churn Prediction
- **Features:** `Age`, `AnnualIncome`, `SpendingScore`, `TotalPurchases`, `TotalSpent`
- **Target:** `ChurnStatus`
- Pipeline with `StandardScaler` + `RandomForestClassifier` (11 trees), evaluated with accuracy

### 3. Clustering: Customer Segmentation
- K-Means with 3 clusters on `Age`, `AnnualIncome`, `SpendingScore`, `TotalPurchases`, `TotalSpent`
- Clusters visualised with scatter plots (Age vs Income, Income vs Spending Score)

### 4. Market Basket Analysis: Apriori
1. Split the `ItemsBought` column into a list of products per customer
2. One-hot encode the transactions using `TransactionEncoder`
3. Mine frequent itemsets with `apriori()` (`min_support = 0.02`)
4. Generate association rules (`min_confidence = 0.1`) and rank them by **support**, **confidence**, and **lift**

**Metrics explained**

- **Support:** how often the itemset appears across all transactions
- **Confidence:** how often the consequent is bought when the antecedent is bought
- **Lift:** strength of the association (lift > 1 means the items are bought together more than by chance)

---

## 📈 Results

| Task | Metric | Score |
|------|--------|-------|
| Linear Regression | R² | **0.948** |
| Random Forest (churn) | Accuracy | **0.995** |
| K-Means | Clusters | 3 |

### Apriori: Market Basket Analysis

Parameters: `min_support = 0.02`, `min_confidence = 0.1`

- **57 frequent itemsets** found (10 single items, 45 pairs, 2 triples)
- **96 association rules** generated

**Top rules by confidence**

| Antecedents | Consequents | Support | Confidence | Lift |
|-------------|-------------|---------|------------|------|
| T-Shirt, Laptop | Headphones | 0.020 | 0.345 | 1.374 |
| Shoes, Smartwatch | Cover | 0.021 | 0.339 | 1.283 |
| Shoes, Cover | Smartwatch | 0.021 | 0.333 | 1.333 |
| Headphones, T-Shirt | Laptop | 0.020 | 0.328 | 1.360 |
| Cover, Smartwatch | Shoes | 0.021 | 0.313 | 1.220 |

All five rules have a lift above 1, meaning these products are bought together more often than expected by chance.

<!-- Optional: add screenshots
![Cluster Plot](images/clusters.png)
-->

---

## 📁 Project Structure

```
ecommerce-ml-analysis/
├── data/
│   └── ecommerce_multitask_dataset.csv
├── ecommerce.ipynb
├── requirements.txt
├── .gitignore
└── README.md
```

---

## ⚙️ Installation & Usage

**1. Clone the repository**

```bash
git clone https://github.com/<your-username>/ecommerce-ml-analysis.git
cd ecommerce-ml-analysis
```

**2. (Optional) Create a virtual environment**

```bash
python -m venv .venv
source .venv/bin/activate      # macOS/Linux
.venv\Scripts\activate         # Windows
```

**3. Install dependencies**

```bash
pip install -r requirements.txt
```

**4. Launch the notebook**

```bash
jupyter notebook ecommerce.ipynb
```

> Make sure the dataset path in the notebook is `data/ecommerce_multitask_dataset.csv`.

---

## 🧰 Tech Stack

- **Language:** Python
- **Data:** pandas, NumPy
- **Visualisation:** Matplotlib, Seaborn
- **Machine Learning:** scikit-learn
- **Association Rules:** mlxtend
- **Environment:** Jupyter Notebook

---

## 💡 Key Learnings

- Apriori needs clean transaction data, so only the product list should be used, not every column in the dataset
- Lift is more reliable than confidence for judging whether a rule is meaningful
- Combining regression, classification, clustering, and association mining on one dataset shows different ways to extract business insight from customer data

---

## 🚀 Future Improvements

- Compare Apriori with FP-Growth
- Tune hyperparameters with cross-validation
- Try additional models (XGBoost, Gradient Boosting)
- Use the elbow method / silhouette score to choose the number of clusters
- Build a simple dashboard (Streamlit) for product recommendations

---

## 👤 Author

**Your Name**
GitHub: (https://github.com/jadhavatharv156-hub)
LinkedIn: (https://www.linkedin.com/in/atharv-jadhav-9a4989280/)

---

⭐ If you found this project useful, consider giving it a star!
