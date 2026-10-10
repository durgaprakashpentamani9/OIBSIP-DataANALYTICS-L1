# Data Cleaning — Oasis Infobyte Level 1 Task 3

## Overview
This project assesses data quality in the supplied 2019 New York City Airbnb listings dataset, documents evidence-based cleaning choices, and exports a separate cleaned CSV.

## Objective
Produce an analysis-ready copy while preserving the original records and distinguishing verified errors from unusual but potentially valid values.

## Dataset source
- Local dataset: `AB_NYC_2019.csv` (CSV; 48,895 rows, 16 columns)
- Location: beside the notebook; this folder did not contain a `data/` directory.
- Dataset title/schema reference: [New York City Airbnb Open Data (Kaggle)](https://www.kaggle.com/datasets/dgomonov/new-york-city-airbnb-open-data). The local file's provenance was not independently confirmed.
- Fields: `id`, `name`, `host_id`, `host_name`, `neighbourhood_group`, `neighbourhood`, `latitude`, `longitude`, `room_type`, `price`, `minimum_nights`, `number_of_reviews`, `last_review`, `reviews_per_month`, `calculated_host_listings_count`, `availability_365`.

## Technologies used
Python, pandas, NumPy, Matplotlib, Seaborn, Jupyter Notebook.

## Features implemented
- Missing-value, duplicate, type, whitespace, category, date-parse, range, and IQR outlier checks.
- Documented treatment of each column with missing data.
- Whitespace normalization, ISO date parsing, reviewed-vs-unreviewed consistency checks, and type comparisons.
- Before/after row, missing, duplicate, and data-type report.
- CSV export and read-back assertions.

## Installation
From this project folder:

```bash
python -m pip install pandas numpy matplotlib seaborn jupyter
```

## How to run the notebook
Open this folder in Jupyter and run all cells in `data_cleaning.ipynb` from top to bottom. Paths are relative to the project folder (and root-folder launch is supported). Outputs are created in `outputs/`.

## Results and important findings
The supplied dataset contains 48,895 rows and 16 columns. Inspection found 16 missing listing names, 21 missing host names, and 10,052 missing values each in `last_review` and `reviews_per_month`. The latter two are aligned: all 10,052 occur on listings with zero reviews. There are no exact duplicate rows or repeated listing IDs. There are 238 names with leading or trailing whitespace, 11 zero-price listings, and no negative prices, minimum-night values below one, negative review counts, availability outside 0–365, or coordinates outside the notebook's broad NYC bounds.

Missing names are marked `[Missing listing name]`; missing host names are marked `[Unknown host]`. Missing review dates remain blank because no review exists. Missing monthly review rates become zero for listings with zero reviews. No records are removed. Outliers flagged by IQR screening are retained because extreme price, minimum-stay, review, or host-listing values are not by themselves proof of invalid records. The 11 zero-price listings are flagged and retained because the source offers no evidence to determine whether they are erroneous.

## Outputs and visualizations
- `outputs/cleaned_data.csv` — cleaned dataset; 48,895 rows retained.
- `outputs/before_after_quality_report.csv` — per-column types and missingness plus row/duplicate counts.
- `outputs/iqr_outlier_report.csv` — IQR fences, counts, and treatment.
- `outputs/iqr_outlier_counts.png` — chart of IQR-flagged values retained.

## Validation status
The notebook's code cells were executed sequentially with the installed Python environment. Assertions and a CSV read-back confirmed row count, unique listing IDs, no duplicate rows, required missing-value treatments, valid checked ranges, and a nonempty export. A Jupyter executable is not installed in this environment, so Jupyter-kernel execution and inline rendering were not independently verified; the saved chart was generated successfully.

## Limitations
The local dataset's original download provenance was not independently verified. The source is a historical 2019 snapshot. IQR is a screening heuristic, and broad coordinate bounds do not constitute full geospatial validation. Unusual values were retained without an external source of truth.

## Conclusion
The cleaned file preserves all 48,895 listings and the original remains unchanged. Missingness and unusual values are explicitly documented, data formatting is standardized where justified, and output quality checks passed.
