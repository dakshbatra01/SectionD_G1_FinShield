#  Notebook 02 – Data Transformation & Feature Engineering Log

##  Input Dataset
- Source: loan_stage1_cleaned.csv

---

##  Step 1: Categorical Value Transformation
Converted encoded values into meaningful labels:

- loan_limit:
  - cf → conforming
  - ncf → non_conforming

- approv_in_adv:
  - nopre → no_preapproval
  - pre → preapproved

- neg_ammortization:
  - not_neg → no
  - neg_amm → yes

- interest_only:
  - not_int → no
  - int_only → yes

- business_or_commercial:
  - b/c → business
  - nob/c → non_business

---

##  Step 2: Outlier Handling
- Applied IQR method on key numerical columns:
  - loan_amount
  - income
  - credit_score
  - ltv
- Removed extreme values to improve data quality

---

##  Step 3: Feature Engineering
Created new features to enhance analysis:

- income_to_loan_ratio:
  - Measures financial strength

- emi_estimate:
  - Approximate loan repayment per term

- emi_income_ratio:
  - Measures affordability

---

##  Step 4: Final Validation
- Checked:
  - Data types
  - Null values
  - Dataset shape
- Ensured dataset consistency and readiness

---

##  Output
- Final dataset saved as:
  - `loan_final_cleaned.csv`

---

##  Summary
This notebook focused on:
- Transforming encoded data into meaningful categories
- Handling outliers
- Creating new analytical features

The dataset is now fully prepared for visualization and analysis.
