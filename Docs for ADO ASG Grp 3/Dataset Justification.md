# Dataset Justification: Contoso Retail DW

### 1. Overview
Our team has selected the **Contoso Retail Data Warehouse** dataset to replace the default North Wind Traders (NWT) sample for Assignment 2. This document outlines how this selection meets and exceeds the complexity requirements while supporting our South East Asia (SEA) expansion strategy.

### 2. Complexity Assessment
The assignment assesses complexity based on Extra Tables, Additional Columns, and Data Depth. The Contoso dataset significantly outperforms the NWT benchmark in all criteria:

* **Factor 1: Extra Tables (13+ vs. 11)**
    * **NWT Benchmark:** 11 Tables.
    * **Contoso Selection:** 13 Tables. We are introducing two separate Fact tables—`FactSales` (Store) and `FactOnlineSales` (E-commerce)—to enable multi-channel analysis. This structure is more complex than the single-stream sales model in NWT.

* **Factor 2: Richer Dimensions (Snowflake Schema)**
    * **NWT Benchmark:** Simple Star Schema with limited columns (76 total).
    * **Contoso Selection:** ~150+ Columns. The Product dimension is normalized into a **Snowflake Schema** (Product → Subcategory → Category). This requires us to implement complex SQL joins and transformation logic during the ELT process, demonstrating advanced DataOps skills.

* **Factor 3: Data Volume & Scalability**
    * **NWT Benchmark:** 3,308 rows.
    * **Contoso Selection:** **~3.4 Million rows** (in `FactSales`).
    * **Justification:** Migrating only 3,000 rows would not sufficiently test the "Scalability" and "Performance Optimization" objectives of the project. Handling 3.4 million rows forces the team to address real-world challenges in cloud storage, loading times, and query performance on Snowflake.

### 3. South East Asia (SEA) Relevance Plan
To fulfill the requirement for a localized context, we will filter and adapt the global Contoso data:

* **Regional Filtering:** We will utilize the `DimGeography` table to isolate transactions specifically for **Singapore, Malaysia, Thailand, and Vietnam**.
* **Strategic Analysis:** Dashboards will compare these specific SEA markets against global performance benchmarks to identify regional growth opportunities.
* **Data Augmentation:** If specific SEA row counts are insufficient for deep analysis, we will strictly follow guidelines to supplement the dataset using GenAI (e.g., generating additional localized transactions for the Singapore region) to ensure meaningful drill-down capabilities.

### 4. Alignment with Project Context
This dataset perfectly mirrors the NWT business case while offering a more realistic "Big Data" environment:
* **Sales Overview:** Covered by `FactSales` and `FactOnlineSales`.
* **Agent Tracking:** Covered by `DimEmployee` linked to specific Store IDs.
* **Supplier/Inventory:** Covered by `DimStore` and Manufacturer data.
