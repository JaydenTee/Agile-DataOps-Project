# Complexity Comparison: Contoso Retail DW vs. NWT

| Metric | NWT Benchmark (Baseline) | Contoso Retail DW (Proposed) | Complexity Factor |
| :--- | :--- | :--- | :--- |
| **Number of Tables** | 11 Tables | **13 Tables** | **Higher:** Meets "Extra tables" requirement. |
| **Total Columns** | 76 Columns | **~150+ Columns** | **Higher:** Richer dimensionality for deep analysis. |
| **Total Rows** | 3,308 Rows | **~3.4 Million Rows** | **Higher:** Significant volume to test cloud scalability. |
| **Relationships** | Simple Star Schema | **Snowflake Schema** | **Higher:** Requires complex SQL joins (Product → Subcat → Category). |
| **Special Entities** | Basic Sales | **Multi-channel** (Online & Store), Promotion, Employee | **Higher:** Adds depth to business logic. |

### 1. Tables (13 Total)
* **2 Fact Tables (Transactional):**
    1.  `FactSales` (In-store transactions)
    2.  `FactOnlineSales` (Online transactions - *Adds complexity NWT doesn't have*)

* **11 Dimension Tables (Context):**
    3.  `DimGeography` (Crucial for SEA)
    4.  `DimStore` (Crucial for SEA)
    5.  `DimEmployee` (Crucial for Agent Tracking)
    6.  `DimProduct`
    7.  `DimProductSubcategory` (*Snowflake Schema structure*)
    8.  `DimProductCategory` (*Snowflake Schema structure*)
    9.  `DimCustomer`
    10. `DimDate` (Required for time intelligence)
    11. `DimPromotion` (Adds "Marketing" context NWT lacks)
    12. `DimChannel` (Online vs Offline context)
    13. `DimCurrency` (Relevant for international/SEA trade)
    
## Why Contoso is More Complex
* **Volume:** Handling 3.4 million rows forces us to implement real DataOps pipelines and performance tuning, unlike the trivial 3,308 rows in NWT.
* **Structure:** The product hierarchy requires multi-level joins, demonstrating advanced SQL capability compared to NWT's flat structure.

<br>

---

# SEA Relevance Plan (South East Asia Focus)

### 1. Key Tables for SEA Insights
To support the requirement for South East Asia relevance, we will utilize the following tables:
* **`DimGeography`**: Contains `RegionCountryName` and `ContinentName` columns. We will filter this dimension to isolate specific SEA markets (e.g., Singapore, Malaysia, Thailand, Vietnam).
* **`DimStore`**: Mapped to `DimGeography`, allowing us to identify the performance of specific physical stores located in the SEA region.
* **`DimEmployee`**: Linked to `DimStore`, enabling "Sales Agent Tracking" specifically for SEA-based staff.

### 2. Strategic Business Questions
Our dashboards will address these specific regional questions:
* **Regional Growth Analysis:** "Which SEA country is driving the highest Year-over-Year (YoY) revenue growth compared to the Global average?"
* **Channel Preference:** "Do customers in Singapore prefer Online purchasing vs. In-Store experience compared to customers in Thailand?"
* **Agent Performance:** "Who are the top 3 Sales Agents in the Singapore region based on high-margin product sales?"


### 3. Data Augmentation Strategy
If the standard Contoso dataset has limited rows for specific SEA countries:
* We will use Generative AI to create supplementary CSV data for `FactSales` representing "New Market Expansion" in Vietnam and Indonesia.
* This ensures we have sufficient data volume to demonstrate meaningful "Drill-down" capabilities in our Power BI dashboards.
