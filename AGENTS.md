# Project Memory & Developer Guidelines

## 📌 Project Overview
- **Project:** Zakat Management and Distribution System Using AI-Based Scoring to Identify the Poorest People
- **Student:** Abu Talha (ID: 0322310105101021), CSE 16th Batch, Pundra University of Science & Technology (PUST), Bogura.
- **Server:** IP `103.125.255.130` (SSH Alias: `zakat-server`, user `root`, configured with ssh key at `~/.ssh/id_ed25519`).
- **Directories on Server:**
  - `/opt/zakat` (Laravel 13 production system, Docker container `zakat-app`)
  - `/opt/zakat-form` (Data collector & training exporter, SQLite db with Bogura data)
  - `/opt/zakat-project` (Academic thesis report, architecture diagrams)

## ⚠️ Core Architectural Principles
1. **Zakat Eligibility is NOT determined by ML.** It is strictly evaluated via Islamic Shariah rules in `app/Services/ZakatEligibilityEngine.php` (Nisab, 8 Asnaf rules, Muslim-only, Syed exclusion).
2. **ML is strictly used for Priority Scoring (0-100)** to rank and identify the poorest people among the eligible beneficiaries so the most needy get aid first.
3. Feature vector consists of 28 features defined in `app/Services/MLScoringService.php`.

## 🚀 Defense Action Plan Reference
Whenever working on the ML or project tasks, refer to [AI_ML_DEFENSE_GUIDE.md](file:///f:/zakat/AI_ML_DEFENSE_GUIDE.md) for the 4-step roadmap (Dataset -> Multi-Model Training -> Visualizations/Metrics -> Laravel Live Integration).
