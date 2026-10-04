# Customer Segmentation & Purchase Behaviour Analysis

## Business questions
Which customers buy recently, repeatedly and at higher value? How do credits affect observed spend? Which differentiated marketing actions could be tested?

## Run
```bash
pip install -r requirements.txt
jupyter notebook Customer_Segmentation.ipynb
```
Run all cells from the repository folder. The input filename is lowercase `data.csv`. Generated files are in outputs/. No Power BI dashboard is required.

## Dataset and provenance
User-supplied transaction CSV, 541,909 original rows with Online Retail schema. Original download provenance was not provided. Reference documentation: https://archive.ics.uci.edu/dataset/352/online+retail . Verify source, currency and reuse terms; schema matching does not establish provenance. Input was supplied as Latin-1 CSV.

## Cleaning and definitions
Exact duplicate rows are removed as a disclosed assumption. Unknown customers are excluded from customer analysis. Invalid fields and exceptions are exported. Explicit service/manual adjustment/fee/gift codes are outside merchandise scope; see notebook and outputs/excluded_codes.csv.

Recency uses last valid purchase relative to the day after the last valid transaction. Frequency counts distinct purchase invoices. Monetary clustering feature is gross positive purchase value. Negative-quantity credits are tracked separately and subtracted for NetSpend; they cannot be matched to original orders. ReturnInvoiceShare is the share of invoice events represented by returns, not an order return probability. CustomerID is never a model feature. Single-order customers retain undefined average purchase gaps and remain eligible.

## Clustering and evaluation
Log1p RFM features are standardized. Compare k=2..6 using silhouette and minimum cluster share (5%); select the highest-scoring qualifying candidate and inspect original-unit profiles. Retain unusual customers, compare capped feature sensitivity and initialization stability. PCA is for visualization only. Cluster labels are descriptive, relative to observed medians and value ranks.

## Results and recommendations
- 4,334 customers with valid purchases entered RFM clustering; customers without purchases remain in the separate metrics export.
- Two clusters were selected from k=2..6, with sampled silhouette 0.434. This differs from the old three-cluster result because feature definitions and population handling were corrected.
- The recent, repeat group contains 1,662 customers (38.35%) and contributes 84.93% of gross merchandise purchase value. Median recency is 17 days, order count 6 and gross value 2,041.33.
- The less-recent, occasional group contains 2,672 customers (61.65%). Median recency is 97 days, order count 1 and gross value 356.92. Re-engagement is a proposed experiment, not a demonstrated benefit.

See outputs/findings.md for verified numerical findings and proposed actions, outputs/segment_profiles.csv for profiles, and outputs/cluster_comparison.csv for cluster choice. No measured sales or retention uplift is claimed.

![Segment profiles](outputs/segment_profiles.png)
![Cluster comparison](outputs/cluster_comparison.png)
![RFM projection](outputs/cluster_projection.png)

The recommendation output preserves segment-popular unseen products. It is a heuristic, not ALS; no predictive recommendation evaluation was performed.

## Key outputs
- customer_segments.csv: one row per purchasing customer, original-unit metrics and segment
- all_customer_metrics.csv: includes return-only customers
- segment_profiles.csv: counts, medians, value shares and proposed actions
- cleaning_audit.csv and transaction_types.csv: population decisions
- cluster_comparison.csv and cluster_sensitivity.csv: clustering evidence
- segment_popularity_recommendations.csv: up to three unseen popular products

## Limitations
Incomplete identities, duplicate ambiguity, manual scope exclusions, unmatched credits and finite observation window. Clusters summarize history and can overlap; recency does not establish churn. Actions require controlled evaluation. Recommendations do not prove relevance. Notebook assertions reconcile values and prevent joins multiplying transactions.
