## 1. Environment Overview
This document summarizes the initial Snowflake environment setup for the Contoso DataOps project.

* **Database:** `CONTOSO_DB`
* **Schemas:**
    * `RAW_CONTOSO`: For raw CSV data ingestion (Bronze Layer).
    * `DW_CONTOSO`: Reserved for transformed dimensional models (Silver/Gold Layer).
* **Role Used:** `TRAINING_ROLE` / `ACCOUNTADMIN` (Check context before running).
* **Stage Name:** `CONTOSO_STAGE` (Internal Named Stage).

## 2. Infrastructure Setup Scripts
### Database & Schema Creation
```sql
CREATE DATABASE IF NOT EXISTS CONTOSO_DB;
USE DATABASE CONTOSO_DB;

CREATE SCHEMA IF NOT EXISTS RAW_CONTOSO;
CREATE SCHEMA IF NOT EXISTS DW_CONTOSO;
```

## 3.Stage & File Format Configuration
### We created a reusable CSV file format that handles headers and empty strings.
```sql
-- Standard File Format
CREATE OR REPLACE FILE FORMAT CSV_CONTOSO_FORMAT
  TYPE = 'CSV'
  FIELD_DELIMITER = ','
  FIELD_OPTIONALLY_ENCLOSED_BY = '"'
  SKIP_HEADER = 1
  NULL_IF = ('NULL', 'null', '')
  ERROR_ON_COLUMN_COUNT_MISMATCH = FALSE;

-- Internal Stage
CREATE OR REPLACE STAGE CONTOSO_STAGE
  FILE_FORMAT = CSV_CONTOSO_FORMAT;
```

## 4.Data Loading (ELT Process)
### Table A: DimProduct
### Source File: DimProduct.csv
### Status: Loaded successfully.
```sql
-- Load Command
COPY INTO RAW_DIMPRODUCT
FROM @CONTOSO_STAGE/DimProduct.csv
FILE_FORMAT = (FORMAT_NAME = CSV_CONTOSO_FORMAT)
ON_ERROR = 'CONTINUE';
```
The COPY INTO command moves data from a stage into a Snowflake table. Data is pulled from a CSV file located at @CONTOSO_STAGE and loaded into the RAW_DIMPRODUCT table using a predefined set of rules called CSV_CONTOSO_FORMAT, which likely handles settings like commas, headers, and null values. By using the ON_ERROR = 'CONTINUE' clause, it will skip any malformed rows and load the remaining valid data rather than aborting the entire process.
## Table B: DimCustomer
### Source File: DimCustomer.csv
### Status: Loaded successfully.
```sql
-- Load Command with Date Fix
COPY INTO RAW_DIMCUSTOMER
FROM @CONTOSO_STAGE/DimCustomer.csv
FILE_FORMAT = (
    TYPE = 'CSV',
    SKIP_HEADER = 1,
    FIELD_OPTIONALLY_ENCLOSED_BY = '"',
    NULL_IF = ('NULL', 'null', ''),
    DATE_FORMAT = 'DD/MM/YYYY',  -- Crucial fix for date parsing
    ERROR_ON_COLUMN_COUNT_MISMATCH = FALSE
)
ON_ERROR = 'CONTINUE';
```
This COPY INTO command moves data from a CSV file in your storage stage into the RAW_DIMCUSTOMER table using specific rules to ensure accuracy. It handles data cleaning by skipping the header, treating empty strings as NULL, and correctly parsing dates in a Day/Month/Year format. By using the CONTINUE error setting and allowing for column count mismatches, the command is designed to be flexible—skipping individual broken rows so that the rest of your data loads without interruption.
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
