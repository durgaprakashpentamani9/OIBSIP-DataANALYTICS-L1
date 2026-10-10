# Customer Segmentation Analysis — Oasis Infobyte Level 1 Task 2

## Overview
This project segments customers from the supplied UCI Online Retail transaction data using K-Means clustering over customer-level Recency, Frequency, and Monetary (RFM) features.

## Objective
Identify groups with different purchase timing, invoice frequency, and observed spend, then suggest a suitable marketing approach for each group.

## Dataset source
- Source: [UCI Machine Learning Repository — Online Retail](https://archive.ics.uci.edu/dataset/352/online+retail)
- Local file: `OnlineRetail.csv` (Latin-1 encoded CSV, 541,909 rows and 8 columns)
- Observed invoice dates: 2010-12-01 to 2011-12-09
- Columns: `InvoiceNo`, `StockCode`, `Description`, `Quantity`, `InvoiceDate`, `UnitPrice`, `CustomerID`, `Country`

The supplied file is kept beside the notebook. No separate `data/` directory was present or assumed.

## Technologies used
Python, pandas, NumPy, Matplotlib, Seaborn, scikit-learn, Jupyter Notebook.

## Features implemented
- Data shape, columns, types, missingness, exact duplicates, cancellation invoices, and invalid quantity/price checks.
- Transparent cleaning for duplicates, cancellation/return lines, invalid purchases, missing customer IDs, and invoice dates.
- Customer RFM features; `AveragePurchaseValue` is also exported as Monetary divided by distinct invoice count.
- `log1p` transformation and `StandardScaler` for RFM clustering features.
- Elbow Method for K=2–8 and reproducible K-Means (`random_state=42`, `n_init=10`, selected K=4).
- Two RFM cluster scatterplot combinations, a customer-count chart, cluster profiles, and marketing actions.

## Installation
From this project directory, install the required packages:

```bash
python -m pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

## How to run the notebook
Open this folder in Jupyter and run all cells in `customer_segmentation.ipynb` from top to bottom. The notebook uses relative paths and writes generated files to `outputs/`.

## Results and important findings
The supplied file has 541,909 transaction rows and 8 columns. Inspection found 5,268 exact duplicates, 9,288 cancellation invoices, 135,080 missing customer IDs, 10,624 rows with quantity <= 0, and 2,517 rows with unit price <= 0. After removing exact duplicate rows and filtering cancellations, nonpositive quantity/price, missing customer IDs, and invalid timestamps, 392,692 purchase lines from 4,338 identified customers remained for RFM.

With reference date 2011-12-10 and selected K=4, the actual cluster means were:

| Cluster | Customers | Mean recency (days) | Mean invoices | Mean observed monetary value |
|---:|---:|---:|---:|---:|
| 0 | 897 | 22.79 | 1.92 | 486.06 |
| 1 | 1,174 | 65.29 | 4.19 | 1,822.98 |
| 2 | 1,549 | 192.27 | 1.35 | 360.55 |
| 3 | 718 | 12.21 | 13.64 | 8,011.89 |

Cluster 3 is the most recent, frequent, and high-spend segment; loyalty recognition and carefully tested cross-sells suit this group. Cluster 2 is least recent with low frequency and spend; a limited win-back campaign is appropriate. Clusters 0 and 1 are more recent or more frequent than Cluster 2 but differ in spend and frequency; use relevant second-purchase, replenishment, and basket-building offers. Review the generated `cluster_profiles.csv` for the notebook's actual per-segment recommendations.

Elbow inertias for K=2–8 were 6476.5, 4858.2, 3925.4, 3269.3, 2841.4, 2533.0, and 2325.1. K=4 is a practical compromise informed by the elbow curve and interpretable profiles, not a claim that four is uniquely optimal.

## Outputs
Running the notebook creates:
- `outputs/elbow_method.png`
- `outputs/cluster_scatterplots.png`
- `outputs/cluster_customer_counts.png`
- `outputs/customer_rfm.csv`
- `outputs/customer_segments.csv`
- `outputs/cluster_profiles.csv`


## Validation status
All notebook code cells were executed sequentially with the installed Python 3.13 environment against the supplied CSV. The generated profiles reconcile to 4,338 customer assignments, and all six output files were checked. A Jupyter executable is not installed in this environment, so inline rendering and a Jupyter-kernel restart-and-run were not verified here; figures were validated through their saved PNG exports.
## Limitations
The file represents a historical period ending in 2011, so behavior may not reflect current customers. Monetary is positive observed revenue for this extract, not lifetime value, and its currency is not explicitly named in the file. Returns/cancellations and unidentified customers are excluded from RFM. K-Means results depend on feature preparation and K; marketing suggestions should be evaluated with controlled campaign tests.

## Conclusion
The transaction history supports interpretable RFM segmentation. Recency separates lapsed from active customers, while invoice frequency and spend identify a smaller highly engaged, high-value group. The notebook produces reproducible cluster assignments, profiles, charts, and segment-specific starting actions.

