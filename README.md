# Personal Expense Tracker with Insights

An end-to-end data analytics portfolio project designed to track, clean, analyze, and visualize personal expenditures. Built with **Python (pandas, matplotlib)** and **SQL (SQLite)** to extract meaningful behavioral spending habits and practical financial insights.

> **Note on Data:** This repository uses a synthesized dummy dataset (`data/raw_expenses.csv`) reflecting one month of realistic student / young adult expenditures in Indian Rupees (INR). You can seamlessly replace it with your own personal financial export by following the [Custom Data Guide](#how-to-use-your-own-data).

---

## Project Highlights & Business Questions Answered

This project answers five practical financial questions that help uncover spending patterns:

1. **Category Distribution:** Which categories account for the largest proportion of total monthly spending?
2. **Weekly Velocity:** How does expenditure fluctuate across the consecutive weeks of the month?
3. **Weekend vs. Weekday Dynamics:** Does discretionary spending spike on weekends, and by what factor?
4. **Payment Rail Preferences:** Which transaction methods (UPI, Cards, Cash) dominate by frequency versus monetary value?
5. **Outlier Identification:** What are the top 5 individual expense transactions and top 3 highest-outflow days?

---

## Visual Analytics & Key Charts

All charts are dynamically generated using `matplotlib` and exported to `outputs/charts/`.

### 1. Spending Breakdown by Category
Food and Shopping represent over 49% of all capital outflow for the month.
![Category Spending](outputs/charts/01_category_spending.png)

### 2. Week-by-Week Spending Trajectory
Spending builds steadily across Weeks 1 and 2, peaking in Week 3 due to project purchases and mid-month obligations.
![Weekly Trend](outputs/charts/02_weekly_trend.png)

### 3. Daily Timeline with Average Benchmark
The baseline average daily burn rate is **₹647 / day**, with distinct spikes during weekends and month-end renewals.
![Daily Timeline](outputs/charts/03_daily_spend_with_average.png)

### 4. Weekday vs Weekend Comparison
While weekdays average ₹490/day, weekends average ₹1,097/day—a **2.24x spending acceleration**.
![Weekday vs Weekend](outputs/charts/04_weekday_vs_weekend.png)

### 5. Payment Method Utilization
UPI dominates transaction count (50 of 77 transactions) and monetary volume (51.9%), while debit/credit cards are reserved for larger purchases.
![Payment Methods](outputs/charts/05_payment_methods.png)

---

## Key Findings Summary

| Metric | Analyzed Value | Context |
| :--- | :--- | :--- |
| **Total Spend** | **₹20,044.00** | Net monthly outlay |
| **Cleaned Transactions** | **77 transactions** | After dropping duplicates and invalid values |
| **Daily Average Outlay** | **₹646.58 / day** | Benchmark required for daily living |
| **Top Category** | **Food (₹5,680.00)** | 28.3% of budget across 33 transactions |
| **Weekend Burn Rate** | **₹1,097.25 / day** | 2.24x higher than weekdays (₹489.83 / day) |
| **Top Payment Rail** | **UPI (51.9%)** | Most frequent mode for micro-purchases |

For full takeaways and strategic budget recommendations, check [outputs/insights.md](outputs/insights.md).

---

## SQL Analysis

The cleaned dataset is exported to an embedded SQLite database (`data/expenses.db`). Six analytical SQL queries in [`sql/queries.sql`](sql/queries.sql) demonstrate core data analyst querying techniques:

- **Aggregations & Ordering (`GROUP BY`, `ORDER BY`):** Summarizing spend volume and transaction frequencies.
- **Group Filtering (`HAVING`):** Isolating categories that exceeded high-budget spending thresholds (₹2,500+).
- **Behavioral Comparison:** Evaluating active days and daily burn rate for weekdays vs. weekends.
- **Single-Row Extremes (`LIMIT`):** Extracting top 5 high-ticket transactions.
- **Subqueries:** Identifying transactions that individually exceeded the overall monthly average expense.
- **Proportional Share:** Calculating the percentage share of each payment rail against the total budget.

---

## Repository Structure

```text
personal-expense-tracker/
│
├── data/
│   ├── raw_expenses.csv         # Synthesized raw dataset with realistic anomalies
│   ├── cleaned_expenses.csv     # Exported post-cleaning dataset
│   └── expenses.db              # SQLite database containing the clean 'expenses' table
│
├── src/
│   └── analysis.py              # Modular Python pipeline (cleaning, EDA, charting, reporting)
│
├── sql/
│   └── queries.sql              # 6 documented SQL queries with explanations
│
├── outputs/
│   ├── insights.md              # Auto-generated markdown report with KPIs & recommendations
│   └── charts/                  # 5 saved high-resolution visualization charts
│       ├── 01_category_spending.png
│       ├── 02_weekly_trend.png
│       ├── 03_daily_spend_with_average.png
│       ├── 04_weekday_vs_weekend.png
│       └── 05_payment_methods.png
│
├── requirements.txt             # Python project dependencies
├── .gitignore                   # Excludes personal data files and cache directories
├── LICENSE                      # MIT Open Source License
└── README.md                    # Project documentation and guide
```

---

## Quickstart Guide

### 1. Prerequisites
Ensure you have Python 3.9+ installed on your system.

### 2. Clone the Repository
```bash
git clone https://github.com/your-username/personal-expense-tracker.git
cd personal-expense-tracker
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Run the Pipeline
Execute the full analysis pipeline with a single command:
```bash
python src/analysis.py
```

This single command will:
1. Load `data/raw_expenses.csv`.
2. Clean messy entries, remove duplicates, impute missing values, and print a cleaning log.
3. Save `data/cleaned_expenses.csv` and create `data/expenses.db`.
4. Render and update all 5 PNG charts in `outputs/charts/`.
5. Generate `outputs/insights.md` with updated KPIs and insights.

---

## How to Use Your Own Data

You can easily adapt this project to analyze your real-world personal bank or UPI expenses:

1. Prepare a CSV file named `raw_expenses.csv` inside the `data/` directory.
2. Ensure your CSV has these 5 headers:
   ```csv
   date,category,description,amount,payment_method
   ```
3. Use `YYYY-MM-DD` date formatting and numeric amounts (no currency symbols in the raw column).
4. Recommended categories: `Food`, `Transport`, `Education`, `Entertainment`, `Shopping`, `Bills`, `Personal Care`.
5. Run `python src/analysis.py` to regenerate your personalized charts and report!

> **Privacy Guard:** The `.gitignore` is already configured to ignore files like `data/my_expenses.csv` or `data/personal_*.csv` so you never accidentally upload sensitive personal bank details to GitHub.

---

## Skills & Competencies Demonstrated

- **Data Wrangling:** Text standardization, string manipulation, date parsing, missing value handling, deduplication with `pandas`.
- **Exploratory Data Analysis (EDA):** Computing summary statistics, frequency distributions, and multi-dimensional segmentations.
- **Data Visualization:** Crafting clear, annotated charts with custom color palettes and benchmark lines using `matplotlib`.
- **Database Querying (SQL):** Constructing queries with aggregations, conditional filtering (`HAVING`), subqueries, and share-of-wallet calculations in SQLite.
- **Analytical Storytelling:** Translating quantitative metrics into actionable real-world financial takeaways.

---

## Next Steps & Future Enhancements

- **Interactive Dashboard:** Build a lightweight dashboard using **Streamlit** to filter expenses dynamically by date and category.
- **Budget Alerts:** Add automatic threshold warnings when a category exceeds 30% of target budget.
- **Automated Ingestion:** Build an automated PDF/SMS parser to convert bank and UPI SMS alerts directly into analysis-ready CSV rows.
