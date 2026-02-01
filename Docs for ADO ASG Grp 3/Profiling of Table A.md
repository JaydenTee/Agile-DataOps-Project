## 5. Primary Key Evaluation, Key Statistics And Observations For Table A DimProduct
### Table A: DimProduct
### Source File: DimProduct.csv
### Status: Loaded successfully.
```sql
SELECT 
    COUNT(*) AS Total_Rows,
    COUNT(DISTINCT ProductKey) AS Unique_Keys,
    (COUNT(*) - COUNT(DISTINCT ProductKey)) AS Duplicate_Keys
FROM RAW_DIMPRODUCT;
```
```sql
-- 3. Date Range Profiling
SELECT 
    MIN(AvailableForSaleDate) AS First_Sale_Date,
    MAX(AvailableForSaleDate) AS Last_Sale_Date
FROM RAW_DIMPRODUCT;

-- 4. Null Checks on Critical Columns
SELECT 
    COUNT(*) AS Null_Names 
FROM RAW_DIMPRODUCT 
WHERE ProductName IS NULL;

-- 5. Data Quality Check (Negative Prices)
SELECT 
    COUNT(*) AS Invalid_Prices 
FROM RAW_DIMPRODUCT 
WHERE UnitPrice < 0 OR UnitCost < 0;

-- 6. Inspect Sample Data
SELECT * FROM RAW_DIMPRODUCT LIMIT 10;
```
