# FinShield

## NST DVA Capstone 2 - Project Repository

> **Newton School of Technology | Data Visualization & Analytics**
> A 2-week industry simulation capstone using Python, GitHub, and Tableau to convert raw data into actionable business intelligence.


## Project Overview

| Field | Details |
|---|---|
| **Project Title** | _FinShield_ |
| **Sector** | _Finance_ |
| **Team ID** | _DVA-G1_ |
| **Section** | _D_ |
| **Faculty Mentor** | _Archit Raj Sir_ |
| **Institute** | Newton School of Technology |
| **Submission Date** | _29 April 2026_ |

### Team Members

| Role | Name | GitHub Username |
|---|---|---|
| Project Lead | _Daksh Batra_ | `dakshbatra01` |
| Data Lead | _Prakhar Rawat_ | `Prakhar13o3` |
| ETL Lead | _Nitin Kumar_ | `Nitin-0017` |
| Analysis Lead | _Isha Tomar_ | `Bytebard089` |
| Visualization Lead | _Kapish Rohilla_ | `kapish9741` |
| Strategy Lead | _Rishi Raj_ | `rishiraj38` |
| PPT and Quality Lead | _Nishant Ranjan Singh_ | `IAmNishantSingh` |

---

## Business Problem

Financial institutions face significant losses due to loan defaults and inefficient borrower screening. This project identifies the key financial and behavioral factors driving loan defaults and develops a data-driven risk segmentation framework to support more effective lending decisions and improved portfolio performance.

**Core Business Question**

> How can we identify high-risk borrowers before loan approval to minimize default rates and financial losses?

**Decision Supported**

> This analysis enables lenders to redesign their loan approval strategy by identifying which borrower profiles should be prioritised, restricted, or offered modified loan terms — replacing the traditional credit-score-first approach with a statistically validated LTV + DTI dual-band policy.

---

## Dataset

| Attribute | Details |
|---|---|
| **Source Name** | _Kaggle_ |
| **Direct Access Link** | _https://www.kaggle.com/datasets/yasserh/loan-default-dataset_ |
| **Row Count** | _15,000_ |
| **Column Count** | _34_ |
| **Time Period Covered** | _2019_ |
| **Format** | _CSV_ |

**Key Columns Used**

| Column Name | Description | Role in Analysis |
|---|---|---|
| `status` | Loan default indicator (0/1) | Target variable |
| `ltv` | Loan-to-Value ratio | Strongest predictor — KPI / Risk Score |
| `debt_to_income_ratio` | Debt-to-Income ratio | Second strongest — KPI / Risk Score |
| `loan_amount` | Total loan amount | EAD / Expected Loss computation |
| `income` | Borrower income | Risk scoring component |
| `credit_score` | Borrower credit score | Validated as non-predictive (p=0.735) |
| `neg_ammortization` | Negative amortisation flag | Strongest categorical risk signal |
| `lump_sum_payment` | Lump sum payment flag | Protective factor |
| `risk_tier` | Computed risk tier | Final lending decision driver |

For full column definitions, see [`docs/data_dictionary.md`](docs/data_dictionary.md).

---

## KPI Framework

| # | KPI | Definition | Target Dashboard |
|---|-----|-----------|------------------|
| 1 | Total Loans | COUNT(*) | Portfolio Exposure & Default Risk Overview |
| 2 | Default Rate | Defaults / Total × 100 | Portfolio Exposure & Default Risk Overview |
| 3 | Total Loan Amount | SUM(loan_amount) | Portfolio Exposure & Default Risk Overview |
| 4 | High Risk % | COUNT(LTV>80) / Total × 100 | Portfolio Exposure & Default Risk Overview |
| 5 | Avg Interest Rate | AVG(rate_of_interest) | Portfolio Exposure & Default Risk Overview |
| 6 | Expected Loss (EL) | Default Rate × LGD × EAD | Portfolio Exposure & Default Risk Overview |
| 7 | Average Income | AVG(income) | Borrower Risk Drivers Analysis |
| 8 | Credit Score Gap | AVG(score, defaulters) / AVG(score, non-defaulters) | Borrower Risk Drivers Analysis |
| 9 | High Borrower Risk % | COUNT(LTV>80) / Total × 100 | Borrower Risk Drivers Analysis |
| 10 | Borrower Income Gap | AVG(income, defaulters) / AVG(income, all) | Borrower Risk Drivers Analysis |
| 11 | Top Loan Purpose | MAX(SUM(defaulted_amount) BY purpose) | Product & Geographic Risk Trends |
| 12 | Average Term | AVG(term) | Product & Geographic Risk Trends |
| 13 | Highest-Loss Region | MAX(SUM(defaulted_amount) BY region) | Product & Geographic Risk Trends |
| 14 | Most Risky Loan Type | MAX(Default Rate BY loan_type) | Product & Geographic Risk Trends |
| 15 | Worst Region–Product Combo | MAX(SUM(defaulted_amount) BY region, loan_type) | Product & Geographic Risk Trends |
| 16 | Loss Share by Purpose | defaulted_per_purpose / total_defaulted × 100 | Product & Geographic Risk Trends |

Full KPI logic is documented in `notebooks/05_final_load_prep.ipynb`.

---

## Tableau Dashboards

| Item | Details |
|---|---|
| **Dashboard URL** | [View Tableau Public Dashboard](https://public.tableau.com/shared/4SBGTH5PQ?:display_count=n&:origin=viz_share_link) |

### 1. Portfolio Exposure & Default Risk Overview
*   **Business Question**: *"How healthy is our current portfolio, and where is our risk concentrated?"*
*   **KPI Cards**: Total Loans, Default Rate, Total Loan Amt, High Risk %, Avg Interest Rate
*   **Charts**: Loan Distribution by Product, Interest Rate vs Default by Loan Purpose, Loan Amount Distribution, Loan Amount by Interest Rate
*   **Filters**: Loan Purpose, Region, Credit Score Bucket

### 2. Borrower Risk Drivers Analysis
*   **Business Question**: *"What borrower characteristics drive default, and how should we adjust underwriting?"*
*   **KPI Cards**: Average Income, Credit Score Gap, High Borrower Risk %, Borrower Income Gap
*   **Charts**: Default Rate by LTV, Default by Income, LTV × Credit Score Heatmap, Loan Volume vs Default Volume by Credit Score, Default Rate by Credit Score Bucket
*   **Filters**: Loan Type, Credit Score Bucket, Region, Approv In Adv, LTV Risk Bucket

### 3. Product & Geographic Risk Trends
*   **Business Question**: *"Which products and regions are bleeding money, and where should we restrict lending?"*
*   **KPI Cards**: Top Loan Purpose, Average Term, Highest-Loss Region, Most Risky Loan Type, Worst Region–Product Combo
*   **Charts**: Loss by Region, Risk vs Pricing by Loan Type, Region × Loan Type Heatmap, Loss Share, Avg DTI by Loan Type, Default Rate by Loan Type
*   **Filters**: Region, Loan Type, Loan Limit, Approv In Adv

Dashboard screenshots are in [`tableau/screenshots/`](tableau/screenshots/) and public links in [`tableau/dashboard_links.md`](tableau/dashboard_links.md).

---

## Key Insights

1. The portfolio default rate is **23.72%**, so reducing default risk must be treated as a primary business objective.
2. `ltv` is the strongest numerical risk signal (`r=0.0976`), indicating high leverage is a key driver of defaults.
3. `debt_to_income_ratio` is the second strongest numerical risk signal (`r=0.0929`), confirming repayment stress as a major default trigger.
4. `credit_score` is not statistically predictive in this dataset (`p=0.735`, `r=-0.0028`), so score-only screening is insufficient.
5. `neg_ammortization` has a strong adverse association with defaults (`χ²=363.1`) and should be tightly controlled.
6. `lump_sum_payment` behaves as a protective factor (`χ²=498.5`) and can be used in safer product structuring.
7. The derived `risk_score` and `risk_tier` framework provides clearer segmentation than single-variable filters, supporting better underwriting decisions.
8. Losses are concentrated in specific segment combinations (region, loan type, and purpose), so targeted controls are more effective than uniform policy actions.

---

## Recommendations

| # | Insight | Recommendation | Expected Impact |
|---|---|---|---|
| 1 | 2, 3 | Implement a dual-threshold underwriting policy using `ltv` and `debt_to_income_ratio` (auto-approve low-risk, review medium-risk, restrict extreme-risk bands). | Lower approval of fragile profiles and improved portfolio default performance. |
| 2 | 4, 7 | Shift from credit-score-first screening to `risk_score` / `risk_tier` based decisioning. | Better alignment between approval decisions and observed default behavior. |
| 3 | 5 | Restrict negative-amortisation loans through stricter eligibility and risk-based pricing controls. | Reduced structural default risk and lower expected loss concentration. |
| 4 | 6 | Offer safer repayment structures (including lump-sum capable plans where suitable) for borderline borrowers. | Improved repayment resilience and reduced delinquency spillover. |
| 5 | 8 | Run a monthly segment watchlist (region × loan type × purpose) and apply targeted lending limits in high-loss pockets. | Faster risk containment and improved capital allocation. |

---

## Repository Structure

```text
SectionD_G1_FinShield/
|
|-- README.md
|
|-- data/
|   |-- raw/                         # Original dataset (never edited)
|   `-- processed/                   # Cleaned output from ETL pipeline
|
|-- notebooks/
|   |-- 01_extraction.ipynb
|   |-- 02_cleaning.ipynb
|   |-- 03_eda.ipynb
|   |-- 04_statistical_analysis.ipynb
|   `-- 05_final_load_prep.ipynb
|
|-- scripts/
|   `-- etl_pipeline.py
|
|-- tableau/
|   |-- screenshots/
|   `-- dashboard_links.md
|
|-- reports/
|   |-- README.md
|   |-- project_report_template.md
|   `-- presentation_outline.md
|
|-- docs/
|   `-- data_dictionary.md
|
|-- DVA-oriented-Resume/
`-- DVA-focused-Portfolio/
```

---

## Analytical Pipeline

The project follows a structured 7-step workflow:

1. **Define** - Sector selected, problem statement scoped, mentor approval obtained.
2. **Extract** - Raw dataset sourced and committed to `data/raw/`; data dictionary drafted.
3. **Clean and Transform** - Cleaning pipeline built in `notebooks/02_cleaning.ipynb` and optionally `scripts/etl_pipeline.py`.
4. **Analyze** - EDA and statistical analysis performed in notebooks `03` and `04`.
5. **Visualize** - Interactive Tableau dashboard built and published on Tableau Public.
6. **Recommend** - 3-5 data-backed business recommendations delivered.
7. **Report** - Final project report and presentation deck completed and exported to PDF in `reports/`.

---

## Tech Stack

| Tool | Status | Purpose |
|---|---|---|
| Python + Jupyter Notebooks | Mandatory | ETL, cleaning, analysis, and KPI computation |
| Google Colab | Supported | Cloud notebook execution environment |
| Tableau Public | Mandatory | Dashboard design, publishing, and sharing |
| GitHub | Mandatory | Version control, collaboration, contribution audit |
| SQL | Optional | Initial data extraction only, if documented |

**Recommended Python libraries:** `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `statsmodels`

---


## Contribution Matrix

This table must match evidence in GitHub Insights, PR history, and committed files.

| Team Member | Dataset and Sourcing | ETL and Cleaning | EDA and Analysis | Statistical Analysis | Tableau Dashboard | Report Writing | PPT and Viva |
|---|---|---|---|---|---|---|---|
| _Daksh Batra_ (Project Lead) | Support | Support | Support | Support | Support | Support | Support |
| _Prakhar Rawat_ (Data Lead) | Owner | Support | Support | Support | Support | Support | Support |
| _Nitin Kumar_ (ETL Lead) | Support | Owner | Support | Support | Support | Support | Support |
| _Isha Tomar_ (Analysis Lead) | Support | Support | Owner | Owner | Support | Support | Support |
| _Kapish Rohilla_ (Visualization Lead) | Support | Support | Support | Support | Owner | Support | Support |
| _Rishi Raj_ (Strategy Lead) | Support | Support | Support | Support | Support | Owner | Support |
| _Nishant Ranjan Singh_ (PPT and Quality Lead) | Support | Support | Support | Support | Support | Support | Owner |

_Declaration: We confirm that the above contribution details are accurate and verifiable through GitHub Insights, PR history, and submitted artifacts._

**Team Lead Name:** Daksh Batra

**Date:** 29 April 2026


*Newton School of Technology - Data Visualization & Analytics | Capstone 2*
