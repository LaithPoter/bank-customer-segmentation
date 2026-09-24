# Bank Customer Segmentation — Iraqi Banking Context

## Overview

An end-to-end **unsupervised learning** project that segments bank customers into distinct groups using **K-Means Clustering**.

What makes this project different from a generic clustering exercise is the dataset context.

The data is **synthetic rather than real customer data**, but it was designed to simulate a realistic **Iraqi banking environment**, including local professions, governorates, income levels, and financial characteristics.

This gives the project a deliberate local-business context while avoiding the privacy and access constraints of real banking customer data.

---

## Why This Dataset Matters

The dataset is not simply a random collection of numbers.

It was built around an Iraqi banking context, with features such as:

- Iraqi governorates
- Local profession categories
- Monthly income in IQD
- Account balances
- Family size
- Education and marital status

That makes the project useful for demonstrating how machine learning can be applied to a **specific local business context**, rather than relying entirely on generic datasets from international benchmarks.

At the same time, the dataset is explicitly **synthetic**.

Therefore, the results should be interpreted as a realistic simulation and portfolio demonstration, **not as evidence about the actual Iraqi banking population**.

---

## Objective

Help a bank understand its customer base beyond a single average customer profile.

Instead of treating every customer identically, segmentation can reveal groups with different combinations of:

- Age
- Income
- Account balance
- Profession
- Education
- Family size
- Work experience
- Location

These segments can then support more targeted financial products, services, and marketing strategies.

---

## Who Is This For?

This type of analysis can be useful for:

- Banks
- Financial institutions
- Marketing teams
- Customer analytics teams
- Product teams

The underlying business idea is simple:

> **Different customer groups may have different financial needs, so treating everyone as one population can hide useful patterns.**

---

## Dataset

`iraqi_bank_customers.csv` contains approximately **4,900 synthetic customer records**.

| Feature | Description |
|---|---|
| `Customer_ID` | Unique customer identifier |
| `Gender` | Male / Female |
| `Ever_Married` | Marital status |
| `Age` | Customer age |
| `Graduated` | Education status |
| `Profession` | Government employee, trader, driver, retired, etc. |
| `Work_Experience` | Years of work experience |
| `Monthly_Income` | Monthly income in IQD |
| `Account_Balance` | Current account balance in IQD |
| `Family_Size` | Number of family members |
| `City` | Iraqi governorate |

### No Target Column — By Design

There is no target/output column.

That is intentional.

This is an **unsupervised learning** problem: the model is not being told what the "correct customer segment" is.

Instead, the algorithm attempts to discover structure in the customer population.

---

## Approach

### 1. Data Understanding

I first checked:

- Dataset shape
- Data types
- Missing values
- Duplicate records

The goal was to understand the structure of the data before applying transformations.

### 2. Exploratory Data Analysis

I used both:

- Manual visual analysis
- Automated profiling with `ydata-profiling`

The EDA covered:

- Distributions
- Correlations
- Categorical breakdowns
- Relationships between financial and demographic variables

This step was important because clustering algorithms can produce groups even when the underlying representation is poorly prepared.

### 3. Feature Engineering

`Customer_ID` was removed before clustering.

This is an important modeling decision.

A customer identifier exists to identify a record — it does not describe the customer's financial behavior, demographics, or needs.

Including it could introduce meaningless numerical structure into the distance calculations used by K-Means.

Binary categorical variables were label-encoded, multi-category variables were one-hot encoded, and the resulting features were standardized using `StandardScaler`.

### 4. Choosing the Number of Clusters

Instead of arbitrarily deciding how many customer groups should exist, I evaluated multiple values of `k` from **2 to 10**.

Two complementary methods were used:

- **Elbow Method**
- **Silhouette Score**

Both were used to reason about an appropriate cluster count, leading to a final choice of **k = 7**.

### 5. K-Means Clustering

The final K-Means model assigned every customer to one of seven clusters.

### 6. Cluster Interpretation

The clusters were not treated as meaningful simply because the algorithm produced them.

Each cluster was profiled using characteristics such as:

- Average age
- Income
- Account balance
- Work experience
- Family size
- Dominant categorical characteristics

This interpretation step converts mathematical clusters into understandable customer profiles.

---

## Key Findings

The strongest relationships in the dataset included:

- `Monthly_Income` ↔ `Account_Balance`
- `Age` ↔ `Work_Experience`
- `Age` ↔ `Account_Balance`

The clustering process produced **7 customer segments**, ranging from young customers with minimal balances to higher-income / higher-balance groups such as traders and retirees.

The analysis also showed different financial patterns across professions:

- Retired customers tended to have higher accumulated balances.
- Traders showed the highest monthly income and balances overall in this dataset.

These are findings **within the synthetic dataset**, not claims about the actual Iraqi population.

---

## Customer Segments

| Cluster | Segment | Example Business Direction |
|---|---|---|
| 0 | Young Students | Starter savings accounts, student debit cards, low-fee products |
| 1 | Low-Income Families | Installment loans, family savings plans |
| 2 | Educated Government Employees | Salary accounts, mid-tier credit cards, home loans |
| 3 | Mid-Income Laborers | Basic savings products, small personal loans |
| 4 | High-Balance Retirees | Investment / deposit products, wealth-management-oriented services |
| 5 | High-Income Traders | Premium banking, business loans, relationship-based services |
| 6 | Private Sector Professionals | Credit cards, auto loans, investment starter products |

These labels are **interpretations of the resulting clusters**, not labels supplied by the dataset.

---

## What I Learned

### 1. An ID column is not a feature

`Customer_ID` is a good example of a column that looks like data but is not actually useful information about the customer.

In K-Means, this matters even more because the algorithm is based on distances.

An arbitrary identifier can create artificial numerical relationships that have nothing to do with customer similarity.

The lesson is:

> **Before asking whether a feature improves the model, ask whether it represents something meaningful.**

### 2. Unsupervised learning requires interpretation

In classification, the target tells you what the model is trying to predict.

Here, there is no target.

That means the difficult part does not end when K-Means returns cluster labels.

The real work is:

**cluster → profile → understand → name → connect to a business context.**

This project helped me understand that clustering is partly a modeling problem and partly an interpretation problem.

### 3. Scaling is essential for distance-based algorithms

K-Means uses distances to determine customer similarity.

If one feature operates on a much larger numerical scale than another, it can dominate those distances.

Standardizing the features therefore was not just a preprocessing formality; it was necessary to make the distance calculations more comparable across variables.

### 4. Choosing `k` should not be arbitrary

Choosing seven clusters simply because seven groups "look useful" would be weak methodology.

Using the Elbow Method and Silhouette Score gave the choice a measurable basis before interpreting the resulting groups.

### 5. A mathematically valid cluster is not automatically a useful business segment

K-Means can produce mathematically distinct groups.

But a bank does not care about cluster numbers.

It cares about whether those groups represent meaningful differences in customer needs and can support decisions about products or services.

That is why cluster profiling and interpretation were treated as a separate step after model fitting.

### 6. Local context can make a portfolio project more meaningful

Using a synthetic Iraqi banking dataset allowed me to demonstrate something beyond the algorithm itself:

**I can take an ML technique and frame it around a specific market and business environment.**

The dataset is fictional, but the context is deliberately realistic enough to explore how customer analytics could be structured for an Iraqi financial institution.

That distinction — **synthetic data, realistic context** — is an important part of the project's credibility.

---

## Limitations

This project should not be interpreted as a study of real Iraqi bank customers.

The dataset is synthetic and was created to simulate a local banking context.

Therefore:

- The discovered segments are properties of this dataset.
- The segment proportions should not be generalized to Iraq's banking population.
- The financial patterns should not be treated as real-world banking statistics.
- Real deployment would require validated customer data, stronger domain knowledge, privacy controls, and ongoing evaluation.

These limitations do not invalidate the project; they define what the project can legitimately claim.

---

## Files

- `bank_customer_segmentation.ipynb` — complete workflow from EDA to clustering and business interpretation
- `iraqi_bank_customers.csv` — synthetic Iraqi-context customer dataset
- `bank_customers_segmented.csv` — final dataset with assigned `Cluster`
- `requirements.txt` — required libraries

---

## Tools

Python · Pandas · Scikit-learn · Matplotlib · Seaborn · ydata-profiling

---

## Author

**Laith Hussein**

[LinkedIn](https://www.linkedin.com/in/laith-hussein-abaub/)
