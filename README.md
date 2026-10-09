# Fraud Transaction Pattern Analysis & Risk Monitoring Dashboard

Project Overview

This end-to-end data analytics project explores transaction patterns
associated with fraud and evaluates transparent, rule-based signals that
could help a fraud-monitoring team prioritize transactions for review.

The project uses **Python (Pandas and Matplotlib)** for data preparation
and exploratory analysis, and **Microsoft Power BI** to build an
interactive dashboard. It does **not** use machine learning.

 Business Question

> Which transaction patterns consistently signal fraudulent behaviour,
> and what triggers should be considered for a real-time fraud alert
> system?

Objectives
-   Analyze fraud patterns across transaction time and day of week.
-   Compare fraud rates across transaction amount ranges.
-   Explore geographic distance as a potential risk signal.
-   Evaluate explainable candidate alert rules and their false-positive
    trade-offs.
-   Present key metrics and patterns in an interactive Power BI
    dashboard.

Tools & Technologies
-   **Python**
-   **Pandas** --- data preparation, feature engineering, grouping, and
    calculations
-   **Matplotlib** --- exploratory visualizations
-   **Microsoft Power BI** --- KPI cards, charts, and interactive
    slicers
-   **Jupyter Notebook / Google Colab** --- analysis environment

Project Structure
Fraud_Transaction_Pattern_Analysis/
├── data/
│   └── fraud_analysis_powerbi.csv
├── notebooks/
│   └── Fraud_Transaction_Pattern_Analysis.ipynb
├── dashboard/
│   └── Fraud_Transaction_Pattern_Analysis.pbix
├── docs/
│   └── Fraud_Transaction_Pattern_Analysis_Project_Report.docx
└── README.md


Dashboard
The Power BI dashboard includes four KPI cards:

-   Total Transactions
-   Fraud Transactions
-   Fraud Rate (%)
-   Fraud Amount

It also includes charts exploring fraud by hour, transaction category,
day of week, amount range, alert priority, and geographic distance
range. Category and alert-priority slicers allow users to filter the
report interactively.

> **Add a dashboard screenshot here:** Save a screenshot of your Power
> BI report in the repository (for example,
> `docs/dashboard_screenshot.png`) and then add:
>
> `![Power BI Dashboard](docs/dashboard_screenshot.png)`

Dataset Summary
The analysis used a sample of **1,000 transactions**, including **69
transactions labelled as fraud**.

  Metric                          Observed result
  ----------------------------- -----------------
  Total transactions                        1,000
  Fraud-labelled transactions                  69
  Overall fraud rate                        6.90%

Key Findings
 1. Time-based patterns

Selected late-night hours showed elevated fraud rates in this sample:

  Hour      Fraud-labelled transactions / total   Observed fraud rate
  ------- ------------------------------------- ---------------------
  22:00                                  7 / 39                17.95%
  00:00                                  8 / 49                16.33%
  02:00                                  6 / 43                13.95%
  01:00                                  6 / 48                12.50%

Tuesday had an observed fraud rate of **10.40%**, while Friday had
**2.74%**. These are sample-specific patterns and should be checked
against larger, representative data before operational use.

2. Transaction amount patterns

Transactions in the **1,000+ amount band** had an observed fraud rate of
**40.00%** (16 fraud-labelled transactions out of 40). This was the
strongest standalone signal among the candidate rules evaluated. Some
higher amount bands contained very few transactions, so their observed
rates are uncertain.

3. Geographic-distance patterns

Transactions at least **250 km** from the reference location had an
observed fraud rate of **10.99%** (31 fraud-labelled transactions out of
282). Distance may be useful as one signal among several, but distance
alone does not prove fraud.

Candidate Alert Rules

The project evaluated three simple, explainable rules:

  --------------------------------------------------------------------------------
  Candidate   Trigger           Flagged   Fraud-labelled     Observed Share of all
  signal                   transactions    among flagged    precision  fraud cases
                                                                          detected
  ----------- ---------- -------------- ---------------- ------------ ------------
  High amount Amount ≥               40               16       40.00%       23.19%
              1,000                                                   

  Long        Distance ≥            282               31       10.99%       44.93%
  distance    250 km                                                  

  High-risk   Hour is               179               27       15.08%       39.13%
  hour        22:00,                                                  
              00:00,                                                  
              01:00, or                                               
              02:00                                                   
  --------------------------------------------------------------------------------

The three signals were also combined into an illustrative priority
scheme:

-   **Critical:** all three signals match
-   **High:** two signals match
-   **Medium:** one signal matches
-   **No candidate signal:** none of these three rules match

In this sample, 52 of 69 fraud-labelled transactions matched at least
one signal (75.36% detection), but this also flagged many legitimate
transactions. All four transactions matching all three signals were
labelled as fraud in this sample; **four cases are far too few to
conclude that this rule will achieve 100% precision in future data**.

Business Recommendations
-   Use amount, time, and distance as **triage signals**, not proof of
    fraud.
-   Consider additional authentication or prompt manual review for
    transactions matching multiple signals.
-   Monitor false positives as well as fraud detection; excessive alerts
    can create customer friction and review costs.
-   Validate candidate thresholds on recent historical data before
    deploying them.
-   Review rule performance regularly as transaction behaviour and fraud
    patterns change.
-   Avoid automatically declining transactions solely on the basis of
    this exploratory analysis.

Methodology
1.  Prepare and inspect the transaction data.
2.  Engineer time-related and geographic features, including hour, day
    of week, weekend indicator, age, and distance.
3.  Compare fraud counts and rates across selected groups and ranges.
4.  Evaluate individual and combined candidate alert rules.
5.  Build an interactive Power BI dashboard to communicate the findings.

Limitations
-   This is a small exploratory sample: 1,000 transactions and 69
    fraud-labelled cases.
-   Results are retrospective and have not been validated on a separate
    holdout dataset or in a live alerting environment.
-   Observed rates may change with a different transaction population.
-   Some amount bands have low transaction counts, which makes their
    rates unstable.
-   The analysis shows associations, not causation. It does not
    establish that any single characteristic causes fraud.
-   Candidate thresholds require further testing and business review
    before real-time use.

How to Explore the Project
1.  Open the notebook in `notebooks/` using Google Colab or Jupyter.
2.  Review the exported analysis data in `data/` if you have permission
    to share and use it.
3.  Open the `.pbix` report in Microsoft Power BI Desktop.
4.  Use the dashboard slicers to explore fraud patterns by category and
    alert priority.

Portfolio Summary
Built an end-to-end fraud transaction pattern analysis project using
Python (Pandas, Matplotlib) and Power BI. Engineered time and geographic
features, evaluated transparent amount/time/distance alert rules,
examined fraud patterns and false-positive trade-offs, and created an
interactive dashboard with KPI cards, charts, and slicers. No
machine-learning model was used.
