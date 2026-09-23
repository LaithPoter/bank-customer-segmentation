# Bank Customer Segmentation using K-Means Clustering

## Overview
An end-to-end unsupervised learning project that segments a bank's customer
base into distinct groups using K-Means clustering. The dataset simulates a
real Iraqi banking context (professions, governorates, and income levels
reflecting the local market).

## Objective
Help banks understand their customer base at a deeper level so they can
design targeted marketing campaigns and match the right financial products
and services to each customer segment, instead of a one-size-fits-all
approach.

## Who is this for?
Banks and financial institutions looking to get more value out of their
customer data by understanding who their customers actually are.

## Dataset
`iraqi_bank_customers.csv` — ~4,900 synthetic customer records with the
following features:

| Column | Description |
|---|---|
| Customer_ID | Unique customer identifier |
| Gender | Male / Female |
| Ever_Married | Marital status |
| Age | Customer age |
| Graduated | Education status |
| Profession | Government employee, trader, driver, retired, etc. |
| Work_Experience | Years of work experience |
| Monthly_Income | Monthly income (IQD) |
| Account_Balance | Current account balance (IQD) |
| Family_Size | Number of family members |
| City | Iraqi governorate |

No target/output column is included on purpose — this is an unsupervised
clustering problem, not a classification one.

## Approach
1. **Data Understanding** — checked shape, types, missing values, duplicates
2. **EDA** — manual visualizations (distributions, correlations, categorical
   breakdowns) + an automated profiling report (`ydata-profiling`)
3. **Feature Engineering** — dropped `Customer_ID`, label-encoded binary
   columns, one-hot encoded multi-category columns, applied `StandardScaler`
   to all features
4. **Model Selection** — used the Elbow Method and Silhouette Score across
   k = 2–10 to choose the optimal number of clusters (k = 7)
5. **K-Means Clustering** — fitted the final model and assigned each
   customer to a cluster
6. **Cluster Interpretation** — profiled each cluster by average age,
   income, balance, work experience, family size, and dominant categories

## Key Findings
- The strongest correlations in the data are between Monthly_Income and
  Account_Balance, Age and Work_Experience, and Age and Account_Balance.
- Retired, older customers hold the highest account balances due to
  accumulated income over time, while traders show the highest monthly
  income and balances overall.
- Clustering revealed 7 distinct customer segments, ranging from young
  students with minimal balances to high-net-worth traders and
  high-balance retirees — segments a bank can target with very different
  products and campaigns.

## Cluster Segments

| Cluster | Segment Name | Recommended Strategy |
|---|---|---|
| 0 | Young Students | Starter savings accounts, student debit cards, low-fee products |
| 1 | Low-Income Families | Installment loans, family savings plans |
| 2 | Educated Government Employees | Salary accounts, mid-tier credit cards, home loans |
| 3 | Mid-Income Laborers | Basic savings products, small personal loans |
| 4 | High-Balance Retirees | Investment/deposit products, wealth management, estate planning |
| 5 | High-Income Traders (VIP) | Premium banking, business loans, dedicated relationship manager |
| 6 | Private Sector Professionals | Credit cards, auto loans, investment starter products |

## Files
- `bank_customer_segmentation.ipynb` — full notebook (EDA → clustering → insights)
- `iraqi_bank_customers.csv` — raw dataset
- `bank_customers_segmented.csv` — final dataset with assigned `Cluster` column
- `requirements.txt` — required libraries

## Tools
Python, Pandas, Scikit-learn, Matplotlib, Seaborn, ydata-profiling

## Author
Laith Hussein
https://www.linkedin.com/in/laith-hussein-abaub/