# E-commerce Data Engineering Pipeline using Databricks

An end-to-end ETL pipeline built with PySpark, Databricks, and Delta Lake using the Bronze-Silver-Gold Medallion Architecture.

## Project Overview

This project implements an end-to-end data engineering pipeline using the Olist Brazilian E-Commerce public dataset. The pipeline processes raw e-commerce data using PySpark and Databricks, transforms it into structured Delta tables, and prepares analytical datasets for reporting.

The project follows the **Medallion Architecture (Bronze, Silver, and Gold)** to organize data processing into multiple layers.

## Tech Stack

- **Language:** Python
- **Processing:** Apache Spark, PySpark
- **Platform:** Databricks
- **Storage Format:** Delta Lake
- **Version Control:** Git and GitHub
- **Dataset:** Olist Brazilian E-Commerce Public Dataset

## Pipeline Architecture

### 1. Bronze Layer — Raw Data Ingestion

- Loaded nine CSV datasets into Databricks.
- Created Bronze Delta tables for customers, orders, order items, payments, products, sellers, reviews, geolocation, and category translation.
- Organized the raw data for downstream processing.

### 2. Silver Layer — Data Cleaning and Transformation

- Removed duplicate orders based on `order_id`.
- Filtered records with missing order identifiers.
- Parsed order purchase timestamps.
- Filtered invalid order-item prices and payment values.
- Aggregated item revenue, freight values, and payments by order.
- Joined order, item, payment, and customer information.
- Created `order_date` and `order_month` columns.

### 3. Gold Layer — Analytical Data

Created analytical Delta tables to support business reporting:

- `gold_olist_sales_by_category` — sales and order metrics by product category.
- `gold_olist_sales_by_city` — order and revenue metrics by customer city and state.
- `gold_olist_sales_by_month` — monthly sales summaries.
- `gold_olist_order_status` — order counts by status.

## Data Quality Validation

The pipeline includes checks for null order identifiers, duplicate orders, missing order dates, and the row counts of Gold tables.

| Validation | Result |
|---|---:|
| Silver orders | 99,441 |
| Null order IDs | 0 |
| Duplicate order IDs | 0 |
| Null order dates | 0 |
| Gold category rows | 74 |
| Gold city/state rows | 4,310 |
| Gold monthly rows | 25 |
| Gold order-status rows | 8 |

These results reflect the validation checks performed during the project run. Further revenue reconciliation and join-grain validation can improve data accuracy.

## Job Execution

The ETL notebook was configured and executed through a Databricks Job. The recorded job run completed successfully with a **Succeeded** status.

## Screenshots

### 1. Successful Databricks Job Run

<img width="1478" height="655" alt="image" src="https://github.com/user-attachments/assets/02f9d7fd-5aca-4cc0-a4c9-bfaa6cef4588" />


### 2. Gold Layer — Sales by Product Category

<img width="1522" height="770" alt="Screenshot 2026-10-17 094103" src="https://github.com/user-attachments/assets/20e3ff1a-2447-4cd6-89d7-7f0ae33770ef" />


### 3. Gold Layer — Sales by City

<img width="1142" height="665" alt="image" src="https://github.com/user-attachments/assets/57e75d75-f3be-47f2-a5e7-4c89ab99a69c" />


### 4. Silver Layer — Cleaned Orders

<img width="1506" height="770" alt="image" src="https://github.com/user-attachments/assets/8b30e171-e25f-4336-92e9-8655f4bb6c98" />


### 5. Data Quality Checks

<img width="1143" height="685" alt="image" src="https://github.com/user-attachments/assets/8475fcea-5f31-48e8-8ef9-cc51e0b689aa" />


## Dataset

This project uses the public Olist Brazilian E-Commerce dataset. Raw CSV files are stored in Databricks and are not included in this repository.

## Key Learnings

- Building a multi-layer data pipeline using the Medallion Architecture.
- Processing CSV data with PySpark.
- Creating and managing Delta tables.
- Performing joins, aggregations, and data-quality checks.
- Organizing transformed data into analytical Gold tables.
- Running a notebook through a Databricks Job.

## Future Improvements

- Add stronger data-quality rules and revenue reconciliation.
- Validate join grain to prevent accidental double-counting.
- Configure scheduled job execution.
- Improve failure handling and monitoring.
- Add further analytical queries and visualizations.
