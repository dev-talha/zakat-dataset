# 📘 Zakat Management and Distribution System Using AI-Based Scoring
> **Academic Project & Research Documentation**  
> **Author:** Abu Talha (ID: 0322310105101021, 16th Batch)  
> **Department:** Department of Computer Science & Engineering (CSE)  
> **Institution:** Pundra University of Science & Technology (PUST), Bogura, Bangladesh  

---

## 🌟 Executive Summary
This project is an enterprise-grade Zakat management web application combined with an **AI-Based Priority Scoring Engine**. It addresses the critical challenges in traditional Zakat distribution—lack of transparency, manual biases, fake claims, and duplicated aid—by bringing Shariah compliance, automated fraud screening, and machine learning into a single cohesive platform.

---

## ⚠️ Core Architectural Principles
1. **Zakat Eligibility is NOT determined by ML:**  
   Eligibility is evaluated exclusively by the **8 Asnaf Shariah Rules Engine** (`ZakatEligibilityEngine.php`), checking Nisab thresholds, 8 Quranic categories, Muslim-only policy, and Syed lineage exclusion.
2. **ML is strictly used for Priority Hardship Scoring (0–100):**  
   Machine Learning ranks verified and eligible beneficiaries based on their poverty severity to ensure that those in the direst need receive assistance first.

---

## 📑 Repository Contents
* 📋 [**System Features List**](docs/PROJECT_FEATURES.md) — Comprehensive functional breakdown of all modules and portals.
* 🧠 [**28-Variable ML Features Specification**](docs/ML_28_FEATURES.md) — Exact data types, descriptions, and mathematical formulas for model training.
* 🎓 [**CSE Final Defense Master Roadmap**](docs/AI_ML_DEFENSE_GUIDE.md) — Step-by-step strategy for dataset generation, model comparison, evaluation metrics, and live demo.
* ⚖️ [**Shariah Rules & 8 Asnaf Specification**](docs/SHARIAH_RULES_ENGINE.md) — Fiqh rules, Nisab thresholds, and global policy gates.

---

## 🛠️ Technology Stack
* **Backend:** PHP 8.3 & Laravel 13 Framework
* **Database:** MySQL 8.4 (54 Eloquent Models, 32 Controllers) & SQLite for Data Collection
* **Frontend:** Responsive Blade Templates, Vite, Tailwind CSS
* **Machine Learning:** Scikit-Learn, XGBoost, Random Forest Regressor (FastAPI / CLI microservice)
* **DevOps:** Docker, Docker Compose, Nginx reverse proxy
* **Integrations:** Porichoy API (NID), bKash Tokenized Checkout, SmsNetBD
