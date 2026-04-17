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
| **Submission Date** | _To be filled by team_ |

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

In the lending sector, financial institutions must decide which borrowers to approve while minimizing the risk of loan defaults. This project is designed for risk analysts and lending managers who need data-driven insights to make better credit decisions. The core challenge is identifying high-risk borrowers early, using historical loan and borrower data. By analyzing patterns in credit behavior, this system helps improve approval strategies and reduce financial losses.

**Core Business Question**

> How can we identify high-risk borrowers before loan approval to minimize default rates and financial losses?

**Decision Supported**

> This analysis enables stakeholders to decide whether to approve, reject, or modify loan applications by assessing the borrower’s default risk, allowing for more informed and risk-aware lending decisions.

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
| _column_1_ | _What it means_ | _Used for KPI / filter / segmentation_ |
| _column_2_ | _What it means_ | _Used for KPI / filter / segmentation_ |
| _column_3_ | _What it means_ | _Used for KPI / filter / segmentation_ |
| _column_4_ | _What it means_ | _Used for KPI / filter / segmentation_ |

For full column definitions, see [`docs/data_dictionary.md`](docs/data_dictionary.md).

---

## KPI Framework

| KPI | Definition | Formula / Computation |
|---|---|---|
| _e.g. Monthly Revenue Growth %_ | _What business outcome this tracks_ | _Show the exact formula or notebook reference_ |
| _e.g. Customer Churn Rate_ | _What business outcome this tracks_ | _Show the exact formula or notebook reference_ |
| _e.g. Repeat Purchase Rate_ | _What business outcome this tracks_ | _Show the exact formula or notebook reference_ |

Document KPI logic clearly in `notebooks/04_statistical_analysis.ipynb` and `notebooks/05_final_load_prep.ipynb`.

---

## Tableau Dashboard

| Item | Details |
|---|---|
| **Dashboard URL** | _Paste Tableau Public link here_ |
| **Executive View** | _Describe the high-level KPI summary view_ |
| **Operational View** | _Describe the detailed drill-down view_ |
| **Main Filters** | _List the interactive filters used_ |

Store dashboard screenshots in [`tableau/screenshots/`](tableau/screenshots/) and document the public links in [`tableau/dashboard_links.md`](tableau/dashboard_links.md).

---

## Key Insights

_List 8-12 major findings from the analysis, written in decision language. Each insight should tell the reader what to think or act upon, not merely describe a chart._

1. _Insight 1_
2. _Insight 2_
3. _Insight 3_
4. _Insight 4_
5. _Insight 5_
6. _Insight 6_
7. _Insight 7_
8. _Insight 8_

---

## Recommendations

_Provide 3-5 specific, actionable business recommendations, each linked directly to an insight above._

| # | Insight | Recommendation | Expected Impact |
|---|---|---|---|
| 1 | _Which insight does this address?_ | _What should the stakeholder do?_ | _What measurable impact do you expect?_ |
| 2 | _Which insight does this address?_ | _What should the stakeholder do?_ | _What measurable impact do you expect?_ |
| 3 | _Which insight does this address?_ | _What should the stakeholder do?_ | _What measurable impact do you expect?_ |

---

## Repository Structure

```text
SectionD_G!_FinShield/
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
| _Member 1_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ |
| _Member 2_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ |
| _Member 3_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ |
| _Member 4_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ |
| _Member 5_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ |
| _Member 6_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ | _Owner / support_ |

_Declaration: We confirm that the above contribution details are accurate and verifiable through GitHub Insights, PR history, and submitted artifacts._

**Team Lead Name:** _____________________________

**Date:** _______________


*Newton School of Technology - Data Visualization & Analytics | Capstone 2*
