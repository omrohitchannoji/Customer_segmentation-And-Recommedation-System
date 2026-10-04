# Verified customer segmentation findings

Input rows: 541,909. RFM eligible customers: 4,334. Reference date: 2011-12-10.
Selected k=2; sampled silhouette=0.434. Groups can overlap; no claim of sharply separated customer types.

- Cluster 0 (Value tier 1/2: less recent, occasional): 2,672 customers (61.7%); median recency 97 days, orders 1, gross value 356.91, net spend 349.62. Proposed action: Test re-engagement messaging; measure incremental purchases.
- Cluster 1 (Value tier 2/2: recent, repeat): 1,662 customers (38.3%); median recency 17 days, orders 6, gross value 2041.33, net spend 1995.04. Proposed action: Test loyalty/service offers and monitor repeat purchases.

## Decisions and limitations
Missing customer identities excluded from customer analysis; exact duplicate removal is an assumption. Merchandise scope excludes listed non-product codes. Credits are not matched to original purchases; net spend is within-window transaction arithmetic. Return-only customers are exported but not clustered. Outliers retained; sensitivity check exported. Recommendations are segment popularity, not ALS. Original upload provenance and currency must be verified against source documentation. Historical clusters do not prove churn, marketing effectiveness or causal effects. Test proposed actions with a suitable controlled evaluation.

All customer, financial, join and recommendation checks passed during execution.