# Customer Churn Analysis & Customer Intelligence

An end-to-end Python notebook for customer churn and retention analysis, segment comparisons, monthly revenue-at-risk estimates, support complaint summaries, and visualizations.

## Features
- Loads source tables from SQLite (`customer_churn.db`) or Excel (`customer_churn_data_raw.xlsx`).
- Validates required columns and key uniqueness.
- Aggregates support records before joining to prevent row multiplication.
- Calculates churn, retention, ARPU, monthly revenue at risk, tenure, escalation rate, and complaint metrics.
- Produces segment summaries, visualizations, a numeric correlation heatmap, and an exported merged CSV.
- Uses clearly labelled synthetic demo data if no source dataset is present, so the notebook can be smoke-tested.

## Requirements
Python 3.10+ recommended.

```bash
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook notebooks/churn_analysis.ipynb
```

## Add your data
Place one of these files in the repository root:

### Option A: SQLite
`customer_churn.db` with tables named `customer`, `subscription`, and `support`.

### Option B: Excel workbook
`customer_churn_data_raw.xlsx` with sheets named `customer`, `subscription`, and `support`.

The customer table must include `customerid` and `state`. The subscription table must include `customerid`, `subscription_start_date`, `cancellation_date`, `plan_type`, and `monthly_charges`. The support table must include `customerid`; `complaint_date` and `escalations` are optional for the corresponding analyses. Additional columns are used when available.

**Privacy:** Do not commit personal/customer data, credentials, database files, or private exports to a public GitHub repository. The included `.gitignore` excludes common local data files.

## Metrics and caveats
- A non-null `cancellation_date` defines churn. Confirm this matches the source system.
- Revenue at risk is the sum of monthly charges for churned customers; it is a monthly-revenue proxy, not lifetime revenue.
- Escalation rate is calculated among customers with a known `Y` or `N` escalation status.
- Correlations are descriptive associations and do not establish causality.
- Synthetic demo results are for code validation only and must not be presented as real business findings.

## Project structure
```text
churn-analysis-github/
├── notebooks/
│   └── churn_analysis.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```
