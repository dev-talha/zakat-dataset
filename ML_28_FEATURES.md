# 🧠 28-Variable Machine Learning Feature Vector Specification

This document defines the 28 input variables extracted by `App\Services\MLScoringService.php` to predict the Poverty Priority Hardship Score (0–100) for eligible beneficiaries.

---

### 📋 1. Demographic & Household Composition
| # | Feature Name | Data Type | Description |
|---|---|---|---|
| **1** | `Total_Family_Members` | Integer | Total number of individuals in the applicant's household |
| **2** | `Number_of_Earning_Members` | Integer | Count of members engaged in gainful employment |
| **3** | `Number_of_Dependent_Members` | Integer | Count of non-earning dependents (children, elderly, infirm) |

---

### 💰 2. Financial & Income Profile
| # | Feature Name | Data Type | Description |
|---|---|---|---|
| **4** | `Family_Monthly_Income_BDT` | Float (BDT) | Total gross monthly household income |
| **5** | `Family_Monthly_Essential_Expense_BDT`| Float (BDT) | Essential survival expenditure (basic food, utilities, clothing) |
| **6** | `Monthly_Assistance_Amount_BDT` | Float (BDT) | External welfare, stipends, or regular aid received |
| **7** | `Monthly_Rent_BDT` | Float (BDT) | Monthly rent paid for shelter |
| **8** | `Net_Assessable_Asset_BDT` | Float (BDT) | Value of assessable liquid/non-essential assets |

---

### 🚨 3. Hardship, Health & Vulnerability Indicators
| # | Feature Name | Data Type | Permitted Values / Description |
|---|---|---|---|
| **9** | `Food_Security_Status` | Categorical | `enough`, `sometimes_insufficient`, `frequently_insufficient`, `regularly_skips_meals`, `no_reliable_food` |
| **10**| `Living_Arrangement` | Categorical | `own_house`, `rented`, `relative`, `disaster_shelter`, `homeless` |
| **11**| `Has_Disability` | Binary | `yes`, `no` (Presence of physical or cognitive disability) |
| **12**| `Has_Serious_Illness` | Binary | `yes`, `no` (Chronic, life-threatening, or debilitating illness) |
| **13**| `Monthly_Medical_Cost_BDT` | Float (BDT) | Recurring essential medical and drug expenses |

---

### ⚖️ 4. Debt & Emergency Hardship
| # | Feature Name | Data Type | Permitted Values / Description |
|---|---|---|---|
| **14**| `Total_Outstanding_Debt_BDT` | Float (BDT) | Cumulative balance of existing unserviced loans |
| **15**| `Net_Unpayable_Debt_BDT` | Float (BDT) | Debt principal that cannot be settled without external aid |
| **16**| `Is_Essential_Need_Debt` | Binary | `yes`, `no` (Borrowed strictly for food, surgery, or shelter) |
| **17**| `Debt_Repayment_Capacity` | Categorical | `yes`, `no`, `partial`, `unknown` |
| **18**| `Is_Disaster_Affected` | Binary | `yes`, `no` (Displaced by flood, river erosion, or cyclone) |
| **19**| `Is_Stranded_Traveler` | Binary | `yes`, `no` (Stranded away from home without funds) |
| **20**| `Has_Access_To_Travel_Funds` | Categorical | `yes`, `no`, `unknown` |

---

### 📐 5. Derived Mathematical Ratios
These engineered ratios provide scale-invariant indicators of poverty severity:

| # | Feature Name | Mathematical Formula | Purpose & Interpretation |
|---|---|---|---|
| **21**| `Per_Capita_Income_BDT` | $\frac{\text{Family Income}}{\text{Total Family Members}}$ | Individual resource allocation per household member |
| **22**| `Monthly_Deficit_BDT` | $\text{Essential Expenses} - \text{Family Income}$ | Absolute monthly cash shortfall |
| **23**| `Income_Coverage_Ratio` | $\frac{\text{Family Income}}{\text{Essential Expense}}$ | Percentage of basic needs met by earnings ($\le 0.20$ = Critical) |
| **24**| `Dependency_Ratio` | $\frac{\text{Dependent Members}}{\text{Earning Members}}$ | Dependency pressure per earner ($\ge 4.0$ = High strain) |
| **25**| `Members_Per_Earner` | $\frac{\text{Total Family Members}}{\text{Earning Members}}$ | Total mouths to feed per breadwinner |
| **26**| `Medical_Cost_Burden_Ratio` | $\frac{\text{Monthly Medical Cost}}{\text{Family Income}}$ | Healthcare drain on monthly cash flow ($\ge 0.30$ = Heavy) |
| **27**| `Unpayable_Debt_Ratio` | $\frac{\text{Unpayable Debt}}{\text{Annual Family Income}}$ | Insolvency metric relative to annual earning power |
| **28**| `Accessible_Asset_Per_Person_BDT`| $\frac{\text{Net Assessable Assets}}{\text{Total Family Members}}$ | Liquid cushion available per family member |
