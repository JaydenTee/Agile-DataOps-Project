## 6. Primary Key Evaluation, Key Statistics And Observations For Table A DimCustomer
### Table B: DimCustomer
### Source File: DimCustomer.csv
### Status: Loaded successfully.
```sql
SELECT 
    COUNT(*) AS total_rows, 
    
    COUNT(DISTINCT CustomerKey) AS unique_customer_keys,
    
    MIN(BirthDate) AS oldest_customer_birth, 
    MAX(BirthDate) AS youngest_customer_birth,
    
    COUNT(*) - COUNT(CustomerKey) AS null_CustomerKey,
    COUNT(*) - COUNT(GeographyKey) AS null_GeographyKey,
    COUNT(*) - COUNT(YearlyIncome) AS null_YearlyIncome,
    
    MIN(YearlyIncome) AS min_income,
    MAX(YearlyIncome) AS max_income
FROM CONTOSO_DB.RAW_CONTOSO.RAW_DIMCUSTOMER;
```
### Profile Summary: RAW_DIMCUSTOMER
```
Relationship to Table DimProduct:
No direct Foreign Key exists between these dimensions.
Both link to the FactSales table via CustomerKey and ProductKey respectively.

Data Quality Observations:
Hidden Nulls: 385 records have names listed as "Not Provided".

Outliers: Massive max income of e.g. $10M and BirthDates dating back to 1910.
Redundancy: Unnamed: 0 column is an unnecessary
```
