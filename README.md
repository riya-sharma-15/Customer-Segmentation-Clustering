# Customer Segmentation using K-Means & PCA

## Project Overview
This project builds an end-to-end **unsupervised machine learning pipeline** for customer 
segmentation on a 2,240-record grocery retail dataset. The goal is to identify distinct 
customer groups based on demographics, spending behaviour, channel preferences, and 
promotion sensitivity — and translate them into **actionable segment-specific strategies** 
for pricing, campaign allocation, and product focus.

---

## Dataset
- **Source:** Customer Personality Analysis (Kaggle)
- **Records:** 2,240 customers
- **Features:** Demographics, product spend (6 categories), purchase channels, 
  campaign response history (5 campaigns), recency

---

## Pipeline

### 1. Data Cleaning
- Median imputation for 24 missing Income values (<1.1% of data)
- Customer tenure (`Customer_For`) calculated from dataset snapshot date for reproducibility
- Outlier treatment via force-fitting (percentile capping) for Income, Age, and spend variables

### 2. Feature Engineering (20+ features)
- Household structure: `num_children`, `has_kids`
- Spend aggregates: `total_spend`, `spend_to_income_ratio`
- Category ratios: per-product spend as share of total spend
- Channel ratios: web, store, catalog purchase proportions
- Deal sensitivity: `deal_purchase_ratio`, `is_discount_heavy`
- Campaign responsiveness: `campaign_accept_count`, `responded_any_campaign`
- Recency flags: `is_recent_customer`, `is_dormant_customer`

### 3. Feature Scaling
- StandardScaler applied before PCA and clustering

### 4. PCA — Dimensionality Reduction
- Systematically evaluated n=1 through n=12 components
- **n=4 selected** as optimal: highest silhouette (0.268) among variance-sufficient 
  configurations (≥60%), retaining 60.7% variance
- PCA clustering outperformed raw feature clustering by **63%** (0.164 → 0.268)
- Each component captures a distinct business dimension:
  - **PC1** — Purchasing power & volume (Income, total_spend, total_purchases)
  - **PC2** — Product preference & lifestyle (Wine/Meat ratios, num_children, web behaviour)
  - **PC3** — Channel behaviour & tenure (store vs web ratio, Customer_For)
  - **PC4** — Campaign engagement & niche categories (campaign_accept_count, Gold/Meat ratios)

### 5. K-Means Clustering
- k=4 selected via Elbow Method and Silhouette Score validation
- `n_init=10` to avoid local minima
- Cluster stability confirmed across 4 random seeds (silhouette variance < 0.0003)
- Cluster profiling performed on **original feature space** (not PCA components) 
  for business interpretability

---

## Final Cluster Profiles

| Cluster | Label | Income | Spend | Key Behaviour |
|---|---|---|---|---|
| **0** | Deal-Influenced High Spenders | 2nd highest | 2nd highest | Highest deal engagement; wine & meat dominant |
| **1** | Premium Elite | Highest | Highest | Campaign-responsive; balanced cross-category spend |
| **2** | Mid-Income Conservatives | Mid | Lowest | Wine-only; campaign-immune; web-active browsers |
| **3** | Low-Income Gold Seekers | Lowest + widest spread | Low-mid | Gold product affinity; occasion-driven gifting |

---

## Model Comparison

| Model | Silhouette | Variance Retained | PCA vs Raw Improvement |
|---|---|---|---|
| PCA n=4 ✅ | **0.268** | 60.7% | **+63%** |
| PCA n=6 | 0.203 | 72.8% | — |
| PCA n=9 | 0.191 | 87.6% | +12.4% |

---

## Key Business Insights
- **Cluster 1** is the only segment with proven multi-campaign ROI — invest in 
  personalised, premium campaigns; never discount
- **Cluster 0** is deal-accelerated, not deal-dependent — structured promotional 
  calendars protect margins while driving volume
- **Cluster 3's** gold product affinity signals a seasonal gifting opportunity 
  largely untapped by standard grocery campaigns
- **Cluster 2** should receive zero outbound campaign spend — low-cost digital 
  passive channels only

---

## Outputs
- PCA explained variance curve and component loadings
- Silhouette and elbow plots for k selection
- Cluster-level feature profiles (income, spend, ratios, channel, campaigns)
- Visualisations: scatter plots, violin plots, bar charts per cluster

---

## Tech Stack
Python, Pandas, NumPy, Scikit-learn, Matplotlib, Seaborn, Plotly
