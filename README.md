# Telco Customer Churn Analysis

![Python](https://img.shields.io/badge/Python-pandas%20%7C%20scipy%20%7C%20matplotlib-3776AB)
![SQL](https://img.shields.io/badge/SQL-SQLite-003B57)
![Excel](https://img.shields.io/badge/Excel-formula--driven-217346)
![Power BI](https://img.shields.io/badge/Power%20BI-DAX%20guide-F2C811)

An end-to-end churn analysis of **7,043 telecom customers**: data cleaning, exploratory analysis, statistical significance testing, and delivery across Python, SQL, Excel, and Power BI.



## Business Question

Which customers are leaving, why, and how much recurring revenue is at risk, answered in a form that analysts, engineers, and business users can each use.

## Key Results

| Metric | Value |
|---|---|
| Customers analyzed | 7,043 |
| Overall churn rate | **26.5%** (1,869 churned) |
| Monthly revenue at risk | **~$139K** |
| Churn: month-to-month contracts | **42.7%** |
| Churn: one-year contracts | 11.3% |
| Churn: two-year contracts | 2.8% |

**Main findings**
- Contract type is the strongest churn driver.
- Churn concentrates in the first 12 months of tenure (0-6 months: 52.9%).
- Fiber-optic customers churn far more than DSL customers despite paying more.
- Electronic-check payers churn at roughly double the rate of autopay customers.
- Among customers with internet add-ons, churn falls as add-ons increase (45.8% with 1 add-on down to 5.3% with 6). Customers with 0 add-ons churn at only 21.4% because that group includes many phone-only customers.
- Every driver above is significant at **p < 0.0001** (chi-square for categorical variables, Welch's t-test for numeric ones).

## Project Structure

```
.
├── data/
│   ├── raw/                        Original source CSV (unmodified)
│   └── processed/                  Cleaned CSV, SQLite DB, insights.json, quality_report.json
├── scripts/
│   └── eda_analysis.py             Cleaning, EDA, stats tests, chart generation
├── sql/
│   └── telco_churn_analysis.sql    11 annotated queries
├── excel/
│   └── Telco_Churn_Analysis.xlsx   KPI summary, churn breakdowns, native charts
├── report/
│   ├── Telco_Churn_Report.docx     Full written report
│   └── Interview_Cheat_Sheet.docx  One-page talking points
├── images/
│   └── dashboard.png               Dashboard preview image
├── figs/                           8 chart PNGs
├── requirements.txt
└── LICENSE
```

## Getting Started

```bash
git clone https://github.com/<your-username>/telco-customer-churn-analysis.git
cd telco-customer-churn-analysis
pip install -r requirements.txt
cd scripts && python eda_analysis.py
```

The script expects the raw CSV as `raw.csv` in the folder you run it from. Copy it first:
`cp ../data/raw/WA_Fn-UseC_-Telco-Customer-Churn.csv raw.csv`

**Run the SQL**
```bash
sqlite3 data/processed/telco.db < sql/telco_churn_analysis.sql
```

**Build the Power BI report**: import `data/processed/telco_cleaned.csv` into Power BI Desktop and follow the DAX measures and visual layout in Section 6 of `report/Telco_Churn_Report.docx`.

## Methodology

1. **Quality checks**: duplicate keys, nulls, category consistency, and a `TotalCharges ≈ tenure × MonthlyCharges` business-rule check.
2. **Cleaning**: merged redundant labels ("No internet service" → "No"); imputed blank `TotalCharges` for zero-tenure customers.
3. **Feature engineering**: `TenureGroup`, `NumAddOns`, `MonthlyChargeBucket`, `ChurnFlag`.
4. **Statistical testing**: chi-square tests (categorical) and Welch's t-tests (numeric), used because churned and retained groups have unequal variance.
5. **Visualization**: bar charts for category comparison, histogram for distribution shape, box plot for spread, heatmap for correlations. Pie, 3D, and dual-axis charts were deliberately avoided.
6. **Delivery**: one deliverable per audience (Python, SQL, Excel, Power BI).

## Tools

| Tool | Used for |
|---|---|
| Python (pandas, scipy, matplotlib, seaborn) | Cleaning, hypothesis tests, charts |
| SQL (SQLite; portable to Postgres, Snowflake, BigQuery) | KPIs, cohorts, window functions |
| Excel (openpyxl) | Live-formula summary workbook |
| Power BI | Setup guide and DAX measures in the report (Section 6); import `data/processed/telco_cleaned.csv` |

## Recommendations

1. Offer incentives to move month-to-month customers onto 1- or 2-year contracts.
2. Add proactive onboarding and outreach during months 0-12.
3. Investigate fiber-optic service quality and price perception.
4. Run an autopay migration campaign for electronic-check payers.
5. Bundle security and tech-support add-ons into entry plans, since churn drops sharply for customers who take several add-ons.

## Data Source

[Telco Customer Churn dataset on Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn), used under its original license.

## License

MIT, see [LICENSE](LICENSE).
