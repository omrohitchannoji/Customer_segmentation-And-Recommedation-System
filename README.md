# 📊 E-Commerce Customer Segmentation & Purchase Behavior Analysis

[![Python 3.8+](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-1.0%2B-orange.svg)](https://scikit-learn.org/)
[![Pandas](https://img.shields.io/badge/Pandas-1.4%2B-150458.svg)](https://pandas.pydata.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

An end-to-end data analytics and customer segmentation project utilizing transactional data to identify high-value customer segments, quantify return behaviors, and derive actionable marketing strategies using **RFM Analysis (Recency, Frequency, Monetary)**, **K-Means Clustering**, and **Market-Basket Popularity Heuristics**.

---

## 📌 Executive Summary

Understanding customer purchase dynamics is critical for maximizing Customer Lifetime Value (CLV) and optimizing marketing spend. This analysis evaluates **541,909 raw transaction records** from an online retail business and segments **4,334 active purchasing customers** using mathematical clustering.

### Key Insights & Findings
* **85/15 Value Concentration**: **38.35% of customers** (Cluster 1: Recent, Repeat) generate **84.93% of total gross merchandise value** ($7,420,418.38).
* **Optimal Segmentation ($K=2$)**: Evaluated $K \in [2, 6]$ using Silhouette Scoring and cluster size constraints ($\ge 5\%$). $K=2$ provided the highest silhouette score (**0.434**), separating customers into distinct value tiers without artificial over-segmentation.
* **Return & Credit Handling**: Credits and returns ($8,506$ line items totaling -$471,750.71) were separated from gross positive sales ($8,737,227.64) to preserve accurate purchase behavior metrics while tracking net spend.
* **Model Stability**: Cluster assignments were validated using **Adjusted Rand Index (ARI)** across multiple random seeds ($\text{ARI} \ge 0.999$) and 99th percentile feature tail capping ($\text{ARI} = 0.9706$).

---

## 🔍 Segment Overview & Comparison

| Metric / Attribute | Cluster 0: Value Tier 1 (Less Recent, Occasional) | Cluster 1: Value Tier 2 (Recent, Repeat) | Overall Population |
| :--- | :---: | :---: | :---: |
| **Customer Count (% Share)** | 2,672 (61.65%) | 1,662 (38.35%) | 4,334 (100.0%) |
| **Median Recency (Days)** | 97.0 days | 17.0 days | 51.0 days |
| **Median Purchase Orders** | 1.0 order | 6.0 orders | 2.0 orders |
| **Median Gross Spend ($)** | $356.92 | $2,041.33 | $662.56 |
| **Median Net Spend ($)** | $349.62 | $1,995.04 | $646.84 |
| **Total Gross Value ($)** | $1,316,809.26 (15.07%) | $7,420,418.38 (84.93%) | $8,737,227.64 (100.0%) |
| **Total Return Value ($)** | $31,886.36 | $435,941.37 | $467,827.73 |
| **Proposed Action** | Test win-back & re-engagement campaigns | Test VIP loyalty/service benefits | Data-driven targeting |

---

## 🛠️ Data Pipeline & Analytics Architecture

```
┌─────────────────────────┐
│ Raw Transactions (541k) │
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐   - Remove Exact Duplicates (5,268 rows)
│ Audited Cleaning        ├─► - Exclude Missing Customer IDs (135,080 rows)
└───────────┬─────────────┘   - Isolate Non-Merchandise Scope (POST, DOT, M, Fees)
            │
            ▼
┌─────────────────────────┐   - Recency: Days to Anchor Date (2011-12-10)
│ RFM Feature Formulation ├─► - Frequency: Distinct Purchase Invoices
└───────────┬─────────────┘   - Gross Monetary: Positive Line Values
            │
            ▼
┌─────────────────────────┐   - Log1p Transformation: log(1 + X)
│ Scaling & Clustering    ├─► - StandardScaler Standardization
└───────────┬─────────────┘   - K-Means Evaluation (K=2..6, Silhouette Scoring)
            │
            ▼
┌─────────────────────────┐   - Segment Profiles & Financial Audits
│ Outputs & Visualizations├─► - Sensitivity Checks (ARI Seed/Cap Validation)
└─────────────────────────┘   - Segment Popularity Recommendation Engine
```

---

## 📈 Visualizations & Model Evaluation

### 1. Segment Profiles Comparison
Medians for recency, order count, and gross purchase value across identified clusters:
![Segment Profiles](outputs/segment_profiles.png)

### 2. K-Means Silhouette Evaluation ($K=2..6$)
Selecting optimal $K$ based on silhouette score maximization and candidate cluster share constraint ($\ge 5\%$):
![Cluster Comparison](outputs/cluster_comparison.png)

### 3. PCA Feature Space Projection
2D projection of standardized $\log(1 + \text{RFM})$ feature space explaining principal variance:
![RFM Projection](outputs/cluster_projection.png)

---

## 🚀 Key Output Files (`outputs/`)

| Output File | Description |
| :--- | :--- |
| [`outputs/customer_segments.csv`](outputs/customer_segments.csv) | Primary customer table with calculated RFM metrics and assigned cluster labels. |
| [`outputs/segment_profiles.csv`](outputs/segment_profiles.csv) | Aggregated medians, totals, revenue shares, and proposed business actions per cluster. |
| [`outputs/cluster_comparison.csv`](outputs/cluster_comparison.csv) | Evaluation table comparing Silhouette scores, Inertia, and min cluster shares for $K=2..6$. |
| [`outputs/cluster_sensitivity.csv`](outputs/cluster_sensitivity.csv) | Stability check results (ARI across seeds and 99th percentile capping). |
| [`outputs/segment_popularity_recommendations.csv`](outputs/segment_popularity_recommendations.csv) | Top-3 unseen popular merchandise recommendations per customer. |
| [`outputs/cleaning_audit.csv`](outputs/cleaning_audit.csv) | Full audit trail tracking row counts and known customer IDs across cleaning stages. |
| [`outputs/findings.md`](outputs/findings.md) | Verified summary report of numerical findings and business recommendations. |

---

## 💡 Business Recommendations & Next Steps

1. **Protect & Nurture High-Value Champions (Cluster 1)**:
   - *Strategy*: Implement dedicated VIP customer support, early access to new product catalog arrivals, and volume-based loyalty benefits.
   - *Rationale*: Cluster 1 drives **84.93% of merchandise value**. Preventing churn in this group is paramount.

2. **Re-Engage Occasional Buyers (Cluster 0)**:
   - *Strategy*: Deploy automated win-back email sequences (e.g., personalized discount incentives on top segment products) timed around day 60–90 post-purchase.
   - *Rationale*: Median recency is **97 days** with only **1 purchase order**. Converting even 10% to repeat buyers yields substantial incremental revenue.

3. **Controlled Experimentation (A/B Testing)**:
   - All proposed marketing actions should be evaluated against control groups to measure true incremental uplift in purchase frequency and revenue.

---

## 💻 Installation & Usage

### Prerequisites
- Python 3.8 or higher
- Jupyter Notebook / JupyterLab

### Running the Analysis
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/omrohitchannoji/Customer_segmentation-And-Recommedation-System.git
   cd Customer_segmentation-And-Recommedation-System
   ```

2. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Execute the Notebook**:
   ```bash
   jupyter notebook Customer_Segmentation.ipynb
   ```
   *Note: Ensure `data.csv` is present in the working directory before running.*

---

## ⚖️ Limitations & Disclaimers

* **Observational Data**: Historical clusters summarize past purchasing behavior and do not establish causal churn predictors.
* **Unmatched Credits**: Return line items (`CreditReturn`) are aggregated within the observation window; credit transactions are not linked to original invoice line items due to dataset schema constraints.
* **Recommendation Engine**: Recommendations use a segment-popularity heuristic (excluding previously bought items), not an ALS matrix factorization model.

---

## 📜 License
Distributed under the MIT License. See `LICENSE` for more information.
