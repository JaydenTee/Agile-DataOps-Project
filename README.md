# Agile DataOps (Assignment 2) - Contoso Retail Cloud Data Transformation

This repository contains the complete end-to-end **DataOps pipeline** for modernizing Contoso Ltd’s global retail data infrastructure. The project migrates a legacy on-premises SQL Server environment to a scalable **Snowflake** cloud data warehouse, culminating in a suite of **Power BI** dashboards for regional stakeholders.

---

## 🏗️ Architecture Overview
The project follows a modern **ELT (Extract, Load, Transform)** architecture designed for infinite scalability and high performance:

* **Ingestion Layer (`RAW_CONTOSO`):** Securely stages and bulk-loads raw CSV datasets into 1:1 replicas of the source system.
* **Integration Layer (`DW_CONTOSO`):** A virtual logic layer utilizing **Star Schema** modeling, performing complex `LEFT JOINS`, data cleaning (placeholder remediation), and deduplication.
* **Presentation Layer (`VIEW_RPT_`):** Secure, optimized views tailored for Power BI DirectQuery, decoupling reporting logic from underlying physical tables.

---

## 🛠️ Tech Stack
* **Data Warehouse:** Snowflake.
* **BI & Visualization:** Power BI.
* **CI/CD & Version Control:** GitHub Actions & GitHub.
* **Trello Board** Traceability
* **Data Management:** Snowflake CLI (SnowSQL).
* **Security:** Key Pair Authentication for secure BI connectivity.

---

## 📂 Repository Structure
The SQL scripts are organized into a strict numeric sequence to enforce dependency order during deployment:

| Script | Purpose |
| :--- | :--- |
| `00_db_and_schemas.sql` | Idempotent setup of the Database and Schema objects. |
| `01_file_formats_and_stage.sql` | Configuration of internal stages and file parsers. |
| `02_load_dimensions.sql` | Ingestion logic for all Dimension tables (Product, Store, etc.). |
| `03_load_facts.sql` | Bulk ingestion for millions of transaction rows into Fact tables. |
| `04_create_master_views.sql` | Transformation layer for data cleaning and business logic. |
| `05_final_reporting_views.sql` | Trusted reporting layer optimized for Power BI. |
| `06_data_quality_validation.sql` | Proof of row counts, integrity checks, and revenue reconciliation. |

---

## 🚀 CI/CD Pipeline
We utilize **GitHub Actions** for automated deployment and validation:
1. **Continuous Integration:** Changes are made via feature branches and merged into `main` after teammate review and approval.
2. **Continuous Deployment:** Merges to `main` trigger an automated workflow that installs required tooling and executes the SQL pipeline in sequence into a `SANDBOX` environment.

---

## 📊 Business Insights
The solution provides five role-specific dashboards to drive decision-making:
* **Chief Financial Officer (CFO):** High-level overview of global revenue ($14.70bn) and profit margins (57.42%).
* **Regional Sales Manager:** Performance tracking across South East Asia hubs like Singapore and Bangkok.
* **Product Owner:** Portfolio analysis identifying "Star" products and inventory liquidation candidates.
* **Operations Manager:** Efficiency monitoring comparing Online vs. Physical sales channel cost ratios.
* **Customer Analyst:** Granular segmentation by demographics (gender, education, occupation) and lifetime value.

---

## 👥 Project Team (Group 3)
* **Ang Shao En:** 
* **Jayden Tee Rong Qing:** 
* **Ho wei Xian:** 
* **Jerremmy Lee Rasni:** 
* **Simon Saw Yong Ping:** 

---
*Developed as part of the Agile DataOps Assignment for Ngee Ann Polytechnic.*
