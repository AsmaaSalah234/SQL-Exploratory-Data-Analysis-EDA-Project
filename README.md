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

## Dimensions Exploration
This step is used to understand the structure of the business data by exploring key dimensions. It helps identify where customers come from geographically and how products are organized. This supports better decision-making in marketing, sales strategy, and product analysis. 

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
