# Exploratory Data Analysis (EDA) Report on Raw Zakat Beneficiary Survey Dataset

**Project Title:** Zakat Management and Distribution System Using AI-Based Scoring to Identify the Poorest People  
**Author:** Abu Talha (Student ID: 0322310105101021, 16th Batch)  
**Academic Affiliation:** Department of Computer Science and Engineering, Pundra University of Science & Technology (PUST), Bogura, Bangladesh  
**Supervision:** Department of CSE, PUST  
**Date of Analysis:** October 2026  
**Dataset File:** raw_dataset.csv  

---

## 1. Executive Summary

This report documents the Exploratory Data Analysis (EDA) conducted on the raw empirical survey dataset (`raw_dataset.csv`) collected across all 12 Upazilas of Bogura District, Bangladesh. The dataset consists of 180 field-surveyed beneficiary applications designed to train machine learning models for poverty priority ranking in an automated Zakat distribution system.

The primary objective of this analysis is to evaluate data completeness, assess distributional properties of key financial and vulnerability indicators, identify data quality anomalies, and establish the preprocessing pipeline required before training regression algorithms.

Key findings include:
- The dataset comprises 180 records across 32 structural columns (24 raw indicators and 8 derived ratio features).
- Geographic representation spans all 12 administrative Upazilas of Bogura, with Bogura Sadar representing the largest cluster (38.9%) and the remaining 11 Upazilas evenly represented (5.5% each).
- Severe financial distress is prevalent across surveyed households, with a median monthly income of BDT 15,200 against a median essential expenditure of BDT 11,675.
- Substantial data cleansing is required due to field-level format heterogeneity, including mixed Bengali-English numerals, embedded currency strings, and multi-lingual categorical values.
- All eight secondary ratio variables are currently unpopulated in the raw export and must be programmatically derived during the feature engineering stage.

---

## 2. Dataset Architecture and Dimensionality

- Total Observations (Rows): 180
- Total Attributes (Columns): 32
- Primary Key: Record_ID (Range: BOG-001 to BOG-180)
- Target Geography: Bogura District, Rajshahi Division, Bangladesh

The attributes are categorized into three operational sets:
1. Identifying and Geographic Metadata: Record_ID, District, Upazila, Union_Area (4 columns)
2. Primary Household, Financial and Vulnerability Variables (20 columns)
3. Derived Hardship Ratios (8 columns)

---

## 3. Geographic Distribution

The survey was structured to capture both urban peri-central households and remote rural riverine (char) populations within Bogura District.

| Upazila | Administrative Type | Observations | Percentage (%) |
|---|---|---|---|
| Bogura Sadar | Urban / Peri-Urban Center | 70 | 38.89% |
| Adamdighi | Western Agrarian Plain | 10 | 5.56% |
| Dhunat | Southern Rural / Riverine | 10 | 5.56% |
| Dupchanchia | North-Western Trade Hub | 10 | 5.56% |
| Gabtali | Eastern Agricultural Region | 10 | 5.56% |
| Kahaloo | Central-Western Rural Plain | 10 | 5.56% |
| Nandigram | Southern Agricultural Belt | 10 | 5.56% |
| Sariakandi | Jamuna Riverine / Flood-Prone Char | 10 | 5.56% |
| Shajahanpur | Southern Industrial / Suburban | 10 | 5.56% |
| Sherpur | Southern Commercial / Agro-Industrial | 10 | 5.56% |
| Shibganj | Northern Horticultural / Archaeological | 10 | 5.56% |
| Sonatola | North-Eastern Char Border | 10 | 5.56% |
| **Total** | **Bogura District Complete** | **180** | **100.00%** |

The sample distribution successfully covers both river-erosion zones (Sariakandi, Sonatola, Dhunat) and high-density wage-labor zones (Bogura Sadar, Shajahanpur).

---

## 4. Data Quality and Cleansing Requirements

Because the survey records were compiled from field interviews conducted by local volunteer enumerators, several structural and syntactic inconsistencies were identified.

### 4.1. Number System Inconsistency
Numeric fields contain an uncontrolled mixture of standard ASCII Arabic numerals (e.g., "5", "12000") and Bengali Unicode numerals (e.g., "৫", "১,২০০", "৩,১০০"). These must be normalized to standard floating-point representation during data ingestion.

### 4.2. Embedded Text and Currency Formatting
Financial columns frequently contain textual artifacts introduced during note-taking:
- Currency prefixes: "BDT", "৳" (e.g., "৳ ৫৫,৬০০", "BDT 15,600").
- Comma separators: "140,150", "3,350".
- Placeholder tokens for unavailable data: "N/A", "অজানা", "—", and empty strings.

### 4.3. Categorical Value Discrepancies
Categorical attributes display multiple lexical variations for identical semantic states:
- Binary Flags (Has_Disability, Has_Serious_Illness, Is_Essential_Need_Debt): Represented interchangeably as "yes", "no", "YES", "NO", "Yes", "No", "হ্যাঁ", "না".
- Food Security Status: Documented using both English terms ("sometimes_insufficient", "regularly_skips_meals", "no_reliable_food", "enough") and Bengali colloquial descriptions ("মাঝে মাঝে কম", "নিয়মিত খাবার বাদ", "নিয়মিত খাবারের ব্যবস্থা নেই", "যথেষ্ট", "পর্যাপ্ত").
- Living Arrangement: Expressed in English ("own_house", "rented", "relative", "disaster_shelter") and Bengali ("নিজ বাড়ি", "ভাড়া বাসা", "আত্মীয়ের বাসায়").

Standardization dictionaries must be mapped to coerce these variations into strictly enumerated factors.

---

## 5. Descriptive Statistical Analysis

The following tables summarize the parametric (Mean, Standard Deviation) and non-parametric (Median, Minimum, Maximum) metrics of the sanitized numerical columns across the 180 observations.

### 5.1. Household Composition Metrics

| Variable | Valid Records | Missing | Mean | Median | Std. Dev. | Min | Max |
|---|---|---|---|---|---|---|---|
| Total_Family_Members | 180 | 0 | 4.84 | 5.00 | 1.82 | 1.00 | 10.00 |
| Number_of_Earning_Members | 179 | 1 | 1.37 | 1.00 | 0.86 | 0.00 | 4.00 |
| Number_of_Dependent_Members | 173 | 7 | 3.46 | 4.00 | 2.01 | 0.00 | 9.00 |

Observations:
- The mean household size is 4.84 members, which aligns closely with Bangladesh Bureau of Statistics (BBS) rural demographic surveys.
- 56.4% of surveyed households rely on a single earning member, while 8.9% report zero stable earning members, indicating severe dependency risk.

### 5.2. Household Financial Profile (in BDT)

| Variable | Valid Records | Missing | Mean | Median | Std. Dev. | Min | Max |
|---|---|---|---|---|---|---|---|
| Family_Monthly_Income_BDT | 179 | 1 | 18,738.83 | 15,200.00 | 14,420.30 | 0.00 | 88,750.00 |
| Family_Monthly_Essential_Expense_BDT | 178 | 2 | 12,010.96 | 11,675.00 | 3,927.21 | 4,650.00 | 27,300.00 |
| Monthly_Assistance_Amount_BDT | 179 | 1 | 667.04 | 0.00 | 1,129.38 | 0.00 | 3,750.00 |
| Monthly_Rent_BDT | 180 | 0 | 1,955.28 | 0.00 | 3,218.74 | 0.00 | 12,100.00 |
| Net_Assessable_Asset_BDT | 174 | 6 | 71,997.41 | 61,100.00 | 54,130.28 | 450.00 | 251,550.00 |
| Monthly_Medical_Cost_BDT | 175 | 5 | 1,721.14 | 500.00 | 3,266.51 | 0.00 | 21,300.00 |
| Total_Outstanding_Debt_BDT | 177 | 3 | 42,007.63 | 41,750.00 | 35,401.47 | 0.00 | 130,100.00 |
| Net_Unpayable_Debt_BDT | 178 | 2 | 13,381.46 | 6,925.00 | 16,977.56 | 0.00 | 90,500.00 |

Observations:
- Net Assessable Assets across all applicants remain well below the standard Islamic Nisab limit (approximately BDT 650,000 for silver equivalent), confirming basic Shariah eligibility for financial aid.
- The maximum medical expenditure observed is BDT 21,300 per month, heavily skewing standard deviation and representing catastrophic health spending.
- The average household indebtedness stands at BDT 42,007.63, with an average of BDT 13,381.46 classified as unpayable essential debt incurred for subsistence survival.

---

## 6. Categorical Vulnerability Distributions

### 6.1. Food Security Status
Food insecurity represents the single most direct indicator of baseline poverty:
- Sometimes Insufficient / Periodic Shortage: 74 households (41.11%)
- Regularly Skips Meals / Moderate Hunger: 39 households (21.67%)
- No Reliable Food / Severe Insecurity: 23 households (12.78%)
- Enough / Food Secure: 42 households (23.33%)
- Unrecorded / Ambiguous: 2 households (1.11%)

Over 75.5% of surveyed families experience active nutritional distress or food rationing.

### 6.2. Living Arrangement and Housing Security
- Own House (Tin-shed, Mud-brick, or Homestead Land): 100 households (55.56%)
- Rented Accommodation (Informal Slum or Sublet): 56 households (31.11%)
- Residing with Relatives / Dependent Shelter: 23 households (12.78%)
- Disaster Relief Shelter: 1 household (0.56%)

Families residing in rented accommodations carry higher cash vulnerability due to unavoidable eviction risks on default.

### 6.3. Physical Disability and Chronic Illness
- Household Member with Physical or Mental Disability: 20 households (11.11%)
- Household Member with Serious / Chronic Debilitating Illness: 30 households (16.67%)

These two factors directly reduce labor availability while creating non-discretionary monthly expenditures.

### 6.4. Debt Repayment Capacity
- Capable of Full Repayment: 102 households (56.67%)
- Capable of Partial Repayment: 41 households (22.78%)
- Completely Incapable of Repayment (Insolvent): 35 households (19.44%)
- Unrecorded: 2 households (1.11%)

---

## 7. Derivation Plan for the Eight Unpopulated Ratio Features

In the raw dataset, columns 25 through 32 are uncalculated (180 null observations). These columns must be populated during preprocessing using the formal deterministic formulas established in the project specification:

1. **Per_Capita_Income_BDT:**
   `Family_Monthly_Income_BDT / Total_Family_Members`
   Evaluates individual living standards irrespective of household aggregate income.

2. **Monthly_Deficit_BDT:**
   `Family_Monthly_Essential_Expense_BDT - (Family_Monthly_Income_BDT + Monthly_Assistance_Amount_BDT)`
   Quantifies the monthly financial shortfall required for survival.

3. **Income_Coverage_Ratio:**
   `(Family_Monthly_Income_BDT + Monthly_Assistance_Amount_BDT) / Family_Monthly_Essential_Expense_BDT`
   Ratios below 1.0 indicate operational insolvency; values below 0.5 denote critical distress.

4. **Dependency_Ratio:**
   `Number_of_Dependent_Members / max(1, Number_of_Earning_Members)`
   Reflects the structural burden borne by active breadwinners.

5. **Members_Per_Earner:**
   `Total_Family_Members / max(1, Number_of_Earning_Members)`
   Normalized demographic dependency scale.

6. **Medical_Cost_Burden_Ratio:**
   `Monthly_Medical_Cost_BDT / max(1, Family_Monthly_Income_BDT)`
   Evaluates the proportion of cash income consumed by pharmaceutical and clinical expenses.

7. **Unpayable_Debt_Ratio:**
   `Net_Unpayable_Debt_BDT / max(1, Family_Monthly_Income_BDT * 12)`
   Debt burden indexed against annualized household income.

8. **Accessible_Asset_Per_Person_BDT:**
   `Net_Assessable_Asset_BDT / Total_Family_Members`
   Per-person asset buffer available prior to total destitution.

---

## 8. Recommendations for Next Engineering Phase

Based on the findings of this exploratory analysis, the following technical milestones should be executed in sequence:

1. **Automated Cleaning Pipeline:** Implement a Python ETL script using pandas to:
   - Convert Bengali Unicode digits to ASCII numeric representations.
   - Strip currency strings and whitespace.
   - Impute missing numeric values using regional medians.
   - Encode categorical attributes using one-hot encoding or ordinal scaling.

2. **Feature Computation:** Calculate the eight derived ratios for all 180 records to complete the 28-variable feature vector.

3. **Label Assignment:** Map reviewed target priority scores (0 to 100) from the expert verification logs.

4. **Model Benchmark Experiments:** Train and cross-validate baseline Linear Regression, Decision Tree Regressor, Random Forest, and XGBoost models on the cleaned matrix to establish initial Mean Absolute Error (MAE) and R-squared performance benchmarks for the defense thesis.

---
*Report prepared for academic defense evaluation, Department of Computer Science and Engineering, Pundra University of Science & Technology (PUST).*
