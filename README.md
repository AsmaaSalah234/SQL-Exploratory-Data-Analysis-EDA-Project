# SQL-Exploratory-Data-Analysis-EDA-Project

This project presents a comprehensive exploratory data analysis (EDA) on a structured sales data warehouse using SQL.
The objective is to analyze sales performance, understand customer behavior, and extract actionable insights that support business decision-making.

The dataset is organized using a **star schema**, consisting of:
- Fact table: `fact_sales`
- Dimension tables:
  - `dim_customers`
  - `dim_products`

Throughout this project, various SQL techniques are applied, including:
- Aggregate functions
- Window functions
- Date functions
- Conditional logic

The analysis is divided into multiple sections, each focusing on a specific business question.

## 📊 Database Exploration
Before starting the analysis, it is essential to understand the structure of the database.

This step helps to:
- Identify available tables
- Understand schemas
- Inspect column-level details
- Prepare for accurate data analysis

## Database Exploration
This step is used to understand the overall structure of the database before starting the analysis. It helps identify all available tables, their schemas, and the metadata of key datasets. This ensures that the analysis is based on a clear understanding of the data model and supports accurate and reliable business insights.

``` sql
/*
===============================================================================
Database Exploration
===============================================================================
Purpose:
    - To explore the structure of the database, including the list of tables and their schemas.
    - To inspect the columns and metadata for specific tables.

Table Used:
    - INFORMATION_SCHEMA.TABLES
    - INFORMATION_SCHEMA.COLUMNS
===============================================================================
*/
-- Retrieve all tables in the database
SELECT 
    TABLE_CATALOG, 
    TABLE_SCHEMA, 
    TABLE_NAME, 
    TABLE_TYPE
FROM INFORMATION_SCHEMA.TABLES;


-- Retrieve column details for dim_customers
SELECT 
    COLUMN_NAME, 
    DATA_TYPE, 
    IS_NULLABLE, 
    CHARACTER_MAXIMUM_LENGTH
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'dim_customers';
```
## Dimensions Exploration  
This step focuses on understanding the structure of the business dimensions. It helps identify customer geography and product hierarchy, which are essential for segmentation, targeting, and performance analysis. This provides a clear view of who the customers are and what products the business offers.
``` sql 
/*
===============================================================================
Dimensions Exploration
===============================================================================
Purpose:
    - To explore the structure of dimension tables.
	
SQL Functions Used:
    - DISTINCT
    - ORDER BY
===============================================================================
*/

-- Retrieve a list of unique countries from which customers originate
SELECT DISTINCT 
    country 
FROM gold.dim_customers
ORDER BY country;

-- Retrieve a list of unique categories, subcategories, and products
SELECT DISTINCT 
    category, 
    subcategory, 
    product_name 
FROM gold.dim_products
ORDER BY category, subcategory, product_name;
```
## Date Range Exploration
This step is used to understand the time coverage of the dataset and key historical boundaries. It helps identify how far the sales data goes back and how recent it is. It also provides insights into customer age distribution, which is useful for segmentation and targeting strategies.
```sql
/*
===============================================================================
Date Range Exploration 
===============================================================================
Purpose:
    - To determine the temporal boundaries of key data points.
    - To understand the range of historical data.

SQL Functions Used:
    - MIN(), MAX(), DATEDIFF()
===============================================================================
*/

-- Determine the first and last order date and the total duration in months
SELECT 
    MIN(order_date) AS first_order_date,
    MAX(order_date) AS last_order_date,
    DATEDIFF(MONTH, MIN(order_date), MAX(order_date)) AS order_range_months
FROM gold.fact_sales;

-- Find the youngest and oldest customer based on birthdate
SELECT
    MIN(birthdate) AS oldest_birthdate,
    DATEDIFF(YEAR, MIN(birthdate), GETDATE()) AS oldest_age,
    MAX(birthdate) AS youngest_birthdate,
    DATEDIFF(YEAR, MAX(birthdate), GETDATE()) AS youngest_age
FROM gold.dim_customers;
```
