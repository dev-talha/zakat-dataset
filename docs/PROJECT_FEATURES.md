# 📋 Zakat Management System — Comprehensive Features List

---

### 🧠 1. AI & Machine Learning Priority Scoring Engine
* **28-Variable Feature Vector Extractor:** Automatically extracts 28 demographic, vulnerability, and financial indicators (e.g., Per Capita Income, Dependency Ratio, Medical Cost Burden Ratio, Food Security Status, Net Unpayable Debt, Asset per Person).
* **0–100 Poverty Priority Scoring:** Computes an objective hardship score to rank eligible beneficiaries so funds reach the most vulnerable first.
* **Dual-Driver Inference Architecture:**
  * **HTTP API Driver (`/predict`):** Connects to external Python ML microservices (XGBoost / Random Forest).
  * **Heuristic Fallback Engine:** Built-in rule-weighted fallback algorithm that ensures uninterrupted scoring even if the ML service is offline.
* **Dedicated Data Collector & Training Exporter (`zakat-form`):**
  * Privacy-safe, PII-free CSV training dataset generation.
  * Inter-rater disagreement filters and median expert scoring labels.

---

### ⚖️ 2. Islamic Shariah Eligibility Rules Engine (8 Asnaf)
*(Strictly rule-based and decoupled from ML to preserve religious compliance)*
* **8 Asnaf Category Rule Evaluator:** Automated conditional assessment for all 8 Quranic categories:
  * *Fakir* (Extreme poverty below Nisab)
  * *Miskin* (Income below basic living expenses)
  * *Gharimin* (Unpayable debt incurred for essential needs)
  * *Ibnus Sabil* (Stranded travelers lacking accessible funds)
  * *Amil, Mu'allaf, Riqab, Fisabilillah* (Specialized administrative & Shariah review workflows)
* **Dynamic Nisab Threshold Check:** Configurable gold/silver Nisab limit (default BDT 650,000) to filter ineligible asset holders.
* **Global Policy Gates:** Strict Muslim-only policy enforcement and Syed lineage exclusion rules.

---

### 🛡️ 3. Multi-Factor Fraud Guard & Security Engine
* **Duplicate NID & Identity Checking:** Prevents same individual applying under multiple profiles.
* **Mobile Number Deduplication:** Flags shared phone numbers across multiple households.
* **Phonetic & Fuzzy Name Matching:** Detects spelling variations and fake aliases using Levenshtein distance, Soundex, and Metaphone algorithms.
* **GPS Cluster & Geo-Anomaly Detection:** Flags suspicious spikes in applications originating from the same coordinates or pinpoint radius.
* **Blacklist & Risk Scoring Pipeline:** Generates `FraudRiskScore` records (0–100) and alerts administrators to high-risk cases.

---

### 👥 4. Multi-Role Portals & Workflow Management
* **Super Admin Portal:** Full system oversight, module toggles, financial ledger, and global policy configurations.
* **Partner Organization Portal:** For NGOs and mosques managing local Zakat campaigns and allocations.
* **Field Volunteer Portal:** Location-based assignment to physically verify applicant households, upload geotagged photos, and inspect living conditions.
* **Donor Transparency Portal:** Enables donors to contribute, track fund utilization, and review anonymized impact reports.
* **Public Beneficiary Portal:** Responsive, multi-step Bengali application wizard with dynamic category-specific questionnaires.

---

### 📦 5. Smart Distribution & Fund Allocation
* **Ranked Priority Queue:** Automatically sorts verified applicants by their ML priority score.
* **Batch / Round Management:** Create distribution rounds (e.g., Ramadan Food Aid, Winter Relief) with defined budgets and beneficiary limits.
* **Double-Dipping Prevention:** Tracks aid history to prevent beneficiaries from receiving overlapping aid across campaigns.
* **Ledger & Audit Trail:** Immutable double-entry bookkeeping for every donation and disbursement.

---

### 🔌 6. Third-Party Service Integrations
* **Porichoy API:** Automated National ID (NID) verification against government records.
* **bKash Tokenized Checkout:** Secure, instant mobile banking payments for donors.
* **SmsNetBD Gateway:** Automated SMS alerts for status updates (application received, volunteer scheduled, grant disbursed).

---

### 💻 7. Technical Infrastructure & Database
* **Backend:** PHP 8.3 & Laravel 13 Framework.
* **Database Models:** 54 Eloquent Models with 32 structured controllers.
* **Frontend:** Responsive Laravel Blade, Vite, and Tailwind CSS.
* **Containerization:** Production Dockerized environment (`zakat-app` & `zakat-form-app`).
