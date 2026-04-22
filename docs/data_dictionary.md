# Data Dictionary — FinShield Loan Default Analysis

This document defines every field used in the analysis and Tableau dashboards. It covers the raw dataset, cleaning decisions, derived columns, and known data quality issues.

---

## Dataset Summary

| Item | Details |
|---|---|
| Dataset name | Loan Default Dataset |
| Source | Kaggle — [Loan Default Dataset](https://www.kaggle.com/datasets/yasserh/loan-default-dataset) |
| Raw file name | `data/raw/Loan_Default.csv` |
| Processed files | `loan_stage1_cleaned.csv`, `loan_final_cleaned.csv`, `loan_tableau_ready.csv` |
| Last updated | April 2026 |
| Granularity | One row per loan application |
| Row count | 15,000 |
| Column count | 34 (raw) → 37 (Tableau-ready) |
| Time period | 2019 |

---

## Column Definitions

### Identifiers

| Column Name | Data Type | Description | Example Value | Used In | Cleaning Notes |
|---|---|---|---|---|---|
| `id` | int | Unique loan application identifier | `49802` | Join key | No nulls; unique across all 15,000 rows |
| `year` | int | Year of loan origination | `2019` | Filter | Single value (2019) — no temporal variation |

### Borrower Demographics

| Column Name | Data Type | Description | Example Value | Used In | Cleaning Notes |
|---|---|---|---|---|---|
| `gender` | string | Gender of the primary applicant | `male`, `female`, `joint`, `NA` | EDA / Tableau | 3,773 missing values filled with `NA`; raw data had `sex not available` |
| `age` | string | Age band of the borrower | `35-44` | EDA / Tableau | Categorical bins: `<25`, `25-34`, `35-44`, `45-54`, `55-64`, `65-74`, `>74` |
| `income` | float | Annual income of the borrower | `1740.0` | KPI / Risk Score / Tableau | No nulls; 540 unique values. Below-median income adds +1 to risk score |

### Loan Characteristics

| Column Name | Data Type | Description | Example Value | Used In | Cleaning Notes |
|---|---|---|---|---|---|
| `loan_limit` | string | Whether the loan conforms to standard limits | `conforming loan` | EDA / Tableau | 2 values. Decoded from raw codes (`cf`, `ncf`) |
| `approv_in_adv` | string | Whether the loan was pre-approved | `no pre-approval` | EDA / Tableau | 2 values. Decoded from raw (`pre`, `nopre`) |
| `loan_type` | string | Type of loan product | `home loan` | KPI / Tableau | 3 values: `home loan`, `personal loan`, `commercial loan`. Decoded from (`type1`, `type2`, `type3`) |
| `loan_purpose` | string | Purpose of the loan | `debt consolidation` | EDA / Tableau | 4 values: `home purchase`, `debt consolidation`, `business purpose`, `refinancing`. Decoded from (`p1`–`p4`) |
| `loan_amount` | int | Total loan amount | `116500` | KPI / EAD / Tableau | No nulls; 150 unique values. Used in Exposure at Default computation |
| `term` | float | Loan term in months | `360.0` | EDA | No nulls; 24 unique terms |
| `rate_of_interest` | float | Annual interest rate | `4.99` | EDA / Tableau | No nulls; 74 unique rates |
| `interest_rate_spread` | float | Spread over the benchmark rate | `1.4474` | EDA | No nulls |
| `upfront_charges` | float | Upfront fees charged at origination | `2463.12` | EDA | Rounded to 2 decimal places during cleaning |
| `property_value` | float | Appraised value of the collateral property | `138000.0` | EDA | No nulls; 244 unique values |

### Credit & Risk Indicators

| Column Name | Data Type | Description | Example Value | Used In | Cleaning Notes |
|---|---|---|---|---|---|
| `credit_worthiness` | string | Internal creditworthiness assessment | `high creditworthy` | EDA / Tableau | 2 values. Decoded from raw (`l1`, `l2`) |
| `credit_type` | string | Credit bureau used for scoring | `experian` | EDA | 4 values: `experian`, `crif`, `cibil`, `equifax`. Decoded from raw |
| `credit_score` | int | Borrower's credit score | `679` | Statistical Analysis | Range ~500–900. **Not predictive of default** (p=0.735, r=-0.0028) |
| `co-applicant_credit_type` | string | Credit bureau of co-applicant | `cib` | EDA | 2 values: `cib`, `exp` |
| `debt_to_income_ratio` | float | Borrower's DTI ratio (%) | `41.0` | KPI / Risk Score / Tableau | Renamed from `dtir1`. Second strongest predictor (r=0.0929) |

### Loan Product Features

| Column Name | Data Type | Description | Example Value | Used In | Cleaning Notes |
|---|---|---|---|---|---|
| `neg_ammortization` | string | Whether loan has negative amortisation | `no` | Risk Score / Tableau | 2 values: `yes`, `no`. Decoded from (`neg_amm`, `not_neg`). Strong risk signal (χ²=363.1) |
| `interest_only` | string | Whether loan is interest-only | `no` | EDA | 2 values: `yes`, `no`. Decoded from (`int_only`, `not_int`) |
| `lump_sum_payment` | string | Whether loan includes lump sum payment option | `no` | Risk Score / Tableau | 2 values: `yes`, `no`. Decoded from (`lpsm`, `not_lpsm`). Protective factor (χ²=498.5) |

### Property & Collateral

| Column Name | Data Type | Description | Example Value | Used In | Cleaning Notes |
|---|---|---|---|---|---|
| `construction_type` | string | Construction type of the property | `sb` | EDA | 2 values: `sb` (site built), `mh` (manufactured housing) |
| `occupancy_type` | string | Occupancy status of the property | `primary residence` | EDA / Tableau | 3 values: `primary residence`, `investment property`, `second residence` |
| `total_units` | string | Number of units in the property | `1u` | EDA | 4 values: `1u`, `2u`, `3u`, `4u` |

### Application & Geography

| Column Name | Data Type | Description | Example Value | Used In | Cleaning Notes |
|---|---|---|---|---|---|
| `open_credit` | string | Whether borrower has open credit lines | `no open credit` | EDA | 2 values. Decoded from (`opc`, `nopc`) |
| `business_or_commercial` | string | Whether the loan is for business or personal use | `business use` | EDA | 2 values. Decoded from (`b/c`, `nob/c`) |
| `submission_of_application` | string | Submission channel | `to_inst` | EDA | 2 values: `to_inst`, `not_inst` |
| `ltv` | float | Loan-to-Value ratio (%) | `84.42` | KPI / Risk Score / Tableau | Strongest numerical predictor of default (r=0.0976, logistic coeff=0.2239) |
| `region` | string | Geographic region | `north` | KPI / Tableau | 4 values: `north`, `south`, `central`, `north-east` |

### Target Variable

| Column Name | Data Type | Description | Example Value | Used In | Cleaning Notes |
|---|---|---|---|---|---|
| `status` | int | Loan default indicator | `0` | Target variable | 0 = No Default, 1 = Default. Default rate = **23.72%** |

---

## Derived Columns

| Derived Column | Logic | Business Meaning |
|---|---|---|
| `ltv_risk_bucket` | Low (≤50), Moderate (50–80), High (80–95), Very High (>95) | Segments borrowers by leverage risk; validated by χ²=491.4 |
| `credit_score_bucket` | Poor (<580), Fair (580–669), Good (670–739), Excellent (740–799), Exceptional (≥800) | Industry-standard credit bands; not predictive in this portfolio (p=0.722) |
| `debt_to_income_ratio` | Renamed from `dtir1` in raw data | Standardised column name for clarity |
| `risk_score` | Weighted composite: DTI>35 (+2), DTI>50 (+4), LTV bucket (Moderate +1, High +2, Very High +3), neg_ammortization=yes (+3), lump_sum=yes (−2), income < median (+1). Floor at 0 | Borrower-level default risk quantification |
| `risk_tier` | Low (≤2), Medium (3–5), High (6–8), Very High (>8) | Categorical risk band driving lending decisions |
| `lending_action` | Low → Approve Standard, Medium → Approve with Conditions, High → Restrict, Very High → Reject/Review | Actionable lending decision per borrower |

---

## Data Quality Notes

- **Gender:** 25.2% of records (3,773) had missing gender. Filled with `NA`.
- **Single time period:** All data is from 2019 — no temporal trends or seasonality can be observed.
- **Class imbalance:** 23.72% default rate. Logistic regression AUC was only 0.596 due to imbalance.
- **Credit score non-predictive:** p=0.735, r=-0.0028 — portfolio-specific finding, should not be generalised.
- **Missing features:** Employment history, repayment track record, and loan vintage are absent from this dataset.
- **Column decoding:** All raw abbreviation codes decoded to readable labels in Notebook 02.
- **Upfront charges:** Rounded to 2 decimal places for consistency.
