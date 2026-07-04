# End-to-End STEM Mentorship Data Pipeline & Analytics Framework

## 📌 Project Overview
This project establishes a low-cost, production-grade Data Engineering and Business Intelligence pipeline for a regional STEM Mentorship Program in South Africa. Facing realistic budget constraints, I bypassed expensive cloud warehouse tools in favor of an optimized Google Workspace & Cloud ecosystem. 

The pipeline automates the extraction of raw session logs, programmatically injects localized demographic data, cleans critical formatting anomalies via Python, and serves a live, interactive 4-page dashboard to departmental stakeholders.

### Key Impact Highlights:
* **Zero-Cost Infrastructure:** Built entirely using free-tier cloud resources, proving scalability under tight budget constraints.
* **Algorithmic Data Enrichment:** Programmatically injected localized geographical and institutional profiles (Pretoria, Joburg, WITS, UP, etc.) to evaluate regional D&I impact.
* **Stakeholder-Driven Design:** Delivered custom views tailored specifically for Operations, Curriculum, Finance, and Outreach executives.

---

## 🛠️ System Architecture
The pipeline follows a classic ETL (Extract, Transform, Load) pattern:

1. **Ingestion (Data Lake/Staging):** Raw CSV data is ingested into a non-converting staging layer in Google Sheets (`Raw_Data`) to preserve formatting anomalies.
2. **Processing & Transformation (ETL Engine):** A Python pipeline built in Google Colab handles secure OAuth2 authentication, reads the staging layer into Pandas, and applies critical business logic.
3. **Data Warehousing (Production):** Cleaned, standardized data is programmatically written to the production database layer (`Clean_Set`).
4. **Analytics & Visualization (BI Layer):** Looker Studio consumes the production layer, offering cross-filtering capabilities for end-users.

---

## 🐍 Data Transformation & Business Logic (Python)
The ETL script (`Mentorship_Data_Pipeline.ipynb`) handles several key production edge cases:
* **Date Standardization:** Coerced mixed-format string dates into a uniform `YYYY-MM-DD` standard.
* **Imputation of Missing Fields:** Identified missing student satisfaction metrics and applied median imputation to prevent artificial skewing of program ratings.
* **Financial Auditing:** Generated a programmatic boolean flag (`Budget_Overrun`) comparing actual expenditures against allocations to immediately surface budget leaks.
* **Demographic Enrichment:** Utilized `numpy` to programmatically simulate a diverse South African cohort across key metros (Mamelodi, Soshanguve, Winterveld, etc.) and universities (UP, WITS, UCT, UJ).

---

## 📊 Looker Studio Interactive Dashboards
The final deliverable is a multi-page, cross-functional dashboard featuring **cross-filtering** capabilities (clicking a chart component automatically filters the entire page view).

### 🛠️ Page 1: Executive Summary & Operations
* **Focus:** Total engagement metrics and operational health.
* **Key Features:** Custom text formatting, hidden index clutter, and a donut-to-table cross-filter isolating student absenteeism.

### 📚 Page 2: Curriculum Performance
* **Focus:** Course delivery success and student satisfaction ratings.
* **Key Features:** Aggregated metric logic transforming raw data sums into true performance averages mapped by STEM fields.

### 💰 Page 3: Financial Health
* **Focus:** Resource efficiency and financial leak detection.
* **Key Features:** Integer-mapped bar charts isolating exact counts of programmatic budget overruns, supported by a bottom-line summary matrix.

### 🌍 Page 4: Diversity & Outreach
* **Focus:** Regional impact and demographic tracking.
* **Key Features:** Stacked column charts and localized donut charts tracking enrollment distributions across South African municipalities.

---

## 🚀 How to Run This Project
1. Clone this repository.
2. Import `data/Raw_Data.csv` into a Google Sheet tab named `Raw_Data` (ensure auto-conversion is turned **off**).
3. Open `Mentorship_Data_Pipeline.ipynb` in Google Colab, authenticate my Google account, and execute the cells to clean and push data to my `Clean_Set` tab.
4. Connect Looker Studio to the production worksheet.
