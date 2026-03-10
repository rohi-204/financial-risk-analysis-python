# 💰 Goldman Sachs — Financial Risk Analysis with Python

![Goldman Sachs](https://img.shields.io/badge/Goldman%20Sachs-Financial%20Risk%20Analysis-003366?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.x-yellow?style=for-the-badge&logo=python)
![pandas](https://img.shields.io/badge/pandas-Data%20Analysis-150458?style=for-the-badge&logo=pandas)
![scipy](https://img.shields.io/badge/scipy-Statistics-8CAAE6?style=for-the-badge&logo=scipy)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

---

## 📌 Project Overview

This project performs end-to-end **financial risk analysis** on Goldman Sachs transaction data using Python. It covers data cleaning, descriptive analysis, customer profiling, risk identification, visualization, and hypothesis testing — all aimed at identifying high-risk accounts and understanding customer financial behavior.

---

## 🎯 Project Objectives

- ✅ Clean and preprocess raw financial transaction data
- ✅ Perform descriptive transactional analysis (monthly/yearly summaries)
- ✅ Build customer profiles based on activity, balance, and transaction volume
- ✅ Identify financial risks — large withdrawals, overdrafts, and anomalies
- ✅ Visualize key insights across transactions, balances, and risk scores
- ✅ Conduct hypothesis testing on account balance vs transaction volume

---

## 📂 Project Structure

```
goldman-sachs-risk-analysis/
│
├── data/
│   ├── goldman_sachs.csv          # Raw dataset
│   └── Cleaned_Data.csv           # Cleaned and preprocessed dataset
│
├── goldman_sachs_analysis.ipynb   # Main notebook (all tasks)
│
└── README.md
```

---

## 🗂️ Dataset Description

| Column | Type | Description |
|---|---|---|
| `TransactionID` | Integer | Unique transaction identifier |
| `CustomerID` | String | Unique customer identifier |
| `AccountID` | String | Unique account identifier |
| `AccountType` | String | Type of account (Credit / Current / Savings) |
| `TransactionType` | String | deposit / withdrawal / payment / transfer |
| `Product` | String | Financial product (e.g. Home Loan, Mutual Fund) |
| `Firm` | String | Associated firm (Firm A / Firm C) |
| `Region` | String | Geographic region of transaction |
| `Manager` | String | Assigned relationship manager |
| `TransactionDate` | Date | Date of the transaction |
| `TransactionAmount` | Float | Amount involved in transaction |
| `AccountBalance` | Float | Account balance at time of transaction |
| `RiskScore` | Float | Customer risk score (0 to 1) |
| `CreditRating` | Integer | Customer credit rating |
| `TenureMonths` | Integer | Customer tenure in months |

---

## 🛠️ Tech Stack

| Category | Tools / Libraries |
|---|---|
| Language | Python 3.x |
| Data Processing | `pandas`, `numpy` |
| Visualization | `matplotlib`, `seaborn` |
| Statistics | `scipy.stats` (ttest_ind, zscore) |
| Date Handling | `datetime` |
| Environment | Jupyter Notebook |

---

## ⚙️ Installation & Setup

**1. Clone the repository**
```bash
git clone https://github.com/yourusername/goldman-sachs-risk-analysis.git
cd goldman-sachs-risk-analysis
```

**2. Install dependencies**
```bash
pip install pandas numpy matplotlib seaborn scipy
```

**3. Run the notebook**
```bash
jupyter notebook goldman_sachs_analysis.ipynb
```

---

## 📋 Task Breakdown

### Task 1 — Data Cleaning & Formatting
- Removed special characters from `TransactionAmount`, `AccountBalance`, and `RiskScore`
- Converted `TransactionDate` to proper datetime format using `pd.to_datetime()`
- Standardized `AccountType` and `TransactionType` to lowercase/stripped format
- Validated all price fields for logical consistency

### Task 2 — Descriptive Transactional Analysis
- Extracted `Month` and `Year` from transaction dates for time-based aggregation
- Built pivot tables to compute monthly totals of deposits, payments, transfers, and withdrawals
- Mapped transaction types to credit/debit categories and plotted monthly trends
- Identified **top 10** and **bottom 10** accounts by net transaction inflow
- Flagged accounts as **Active / Inactive** based on 60+ day gaps between consecutive transactions

### Task 3 — Customer Profile Building
- **Activity Segmentation** (Rubric: High > 20 txns, Medium ≥ 10, Low < 10)
- **Customer Segmentation** by average balance & total transaction volume (4 quadrants):
  - High Balance – High Volume
  - High Balance – Low Volume
  - Low Balance – High Volume
  - Low Balance – Low Volume
- Identified **high net inflow** accounts (TotalCredit > TotalDebit)
- Flagged **high-frequency low-balance** accounts as potential upsell or risk targets
- Detected accounts with **negative or near-zero balances** (≤ ₹1,000)

### Task 4 — Financial Risk Identification
- Flagged accounts with large withdrawals (> ₹50,000)
- Tracked accounts with overdraft transactions (`AccountBalance < 0`)
- Calculated **balance volatility** using Coefficient of Variation (CV)
  - CV > 0.5 → High volatility / Risky account
  - CV ≤ 0.5 → Stable account
- Applied **IQR method** for anomaly detection on transaction amounts
- Combined all risk signals to produce a final `SuspiciousFlag` (Suspicious / Normal)

### Task 5 — Visualisation
- Distribution of Transaction Amounts (histogram + KDE)
- Transaction Type Distribution (bar chart)
- Monthly Transaction Count Trend (line chart)
- Transaction Amount vs Account Balance (scatter plot)
- Distribution of Balance Volatility / CV (histogram + KDE)
- Activity Level vs Average Balance (box plot)
- Risk Score Distribution (histogram + KDE)

### Task 6 — Hypothesis Testing
- **H₀:** No significant difference in average balance between high-volume and low-volume accounts
- **H₁:** High-volume accounts have significantly higher average balances
- **Method:** Welch's independent t-test (`equal_var=False`)
- **Result:** T-statistic = 0.315, P-value = 0.753 → **Fail to Reject H₀**
- **Conclusion:** Transaction volume does not significantly predict account balance

---

## 📊 Key Findings

| Finding | Detail |
|---|---|
| **Top Account** | ACC46655 with net inflow of ₹728,037 |
| **Negative Balance** | ACC19178 with avg balance of -₹1,541 |
| **Most Volatile** | Accounts with CV > 0.5 flagged as high-risk |
| **Suspicious Accounts** | Flagged based on large withdrawals + overdrafts + anomalies |
| **Debit >> Credit** | Monthly debit volumes consistently exceed credit volumes |
| **Hypothesis Result** | No link between transaction frequency and account balance (p = 0.75) |

---

## 📉 Visualizations Included

- 📊 Distribution of Transaction Amounts
- 📊 Transaction Type Distribution
- 📈 Monthly Transaction Count Trend
- 🔵 Transaction Amount vs Account Balance (Scatter)
- 📊 Distribution of Balance Volatility (CV)
- 🟩 Activity Level vs Average Balance (Boxplot)
- 🟠 Risk Score Distribution

---

## 💡 Recommendations

- Focus risk monitoring on accounts with **CV > 0.5** and repeated large withdrawals
- Target **high-frequency low-balance** customers for financial wellness products
- Investigate accounts with **negative balances** for potential credit risk action
- Use the **SuspiciousFlag** model as a first-pass fraud/risk screening layer
- Incorporate external data (credit bureau scores, macroeconomic indicators) for richer profiling

---

## 📬 Contact

For queries or collaboration, feel free to reach out via GitHub Issues or Pull Requests.
