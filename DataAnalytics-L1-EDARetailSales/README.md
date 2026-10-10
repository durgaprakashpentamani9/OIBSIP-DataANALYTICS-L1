# Exploratory Data Analysis on Retail Sales Data

## Overview
An exploratory analysis of 1,000 retail transactions for the Oasis Infobyte Data Analytics Internship Project 1.

## Objective
Describe sales trends, demographic patterns, and category performance; identify data limitations; and provide evidence-based business recommendations.

## Dataset source
The supplied CSV is included at `data/retail_sales_dataset.csv` for a self-contained project. The internship specification suggests the [Kaggle Retail Sales Dataset](https://www.kaggle.com/datasets/mohammadtalib786/retail-sales-dataset). The inspected file has 1,000 rows and 9 columns, no missing values, and no exact duplicate rows.

## Technologies used
Python, pandas, NumPy, Matplotlib, Seaborn, and Jupyter Notebook.

## Features implemented
- Data structure, missing-value, duplicate, data-type, and transaction arithmetic checks.
- Mean, median, mode, and standard deviation for numeric fields.
- Monthly and quarterly revenue trends.
- Age-group and gender analysis.
- Revenue and quantity analysis by category.
- Correlation heatmap and weekday transaction-value visualization.
- Written chart observations, limitations, and three actionable recommendations.

## Installation
From the project directory, install the notebook dependencies:

```bash
python -m pip install pandas numpy matplotlib seaborn jupyter
```

## How to run
Open a terminal in this directory and run:

```bash
jupyter notebook retail_sales_eda.ipynb
```

Run the cells from top to bottom. All data and chart paths are relative to this folder.

## Results and important findings
- 1,000 transactions and 456,000 revenue units; no missing values or exact duplicate rows.
- Electronics had the highest category revenue (156,905); Clothing had the most transactions (351).
- May 2023 was the strongest month (53,150). January 2024 contains only one day's data.
- Saturday had the highest average transaction amount (525.43), a pattern to validate before acting on it.

## Screenshots or visualizations
Generated chart exports are in [`outputs/`](outputs/): monthly and quarterly trends, customer demographics, category revenue, numerical correlations, and weekday transaction value.

## Limitations
The file has categories but no product names, so it cannot support individual top-10 products. Customer IDs are unique per row, preventing repeat-purchase analysis. Currency is unspecified, and revenue is not profit. January 2024 is partial.

## Conclusion
The analysis identifies category, time, and demographic patterns to guide inventory review and controlled marketing tests. Recommendations should be validated with longer histories, product-level data, cost/margin fields, and experimental measurement.
