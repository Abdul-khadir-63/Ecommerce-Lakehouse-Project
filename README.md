# Ecommerce-Lakehouse-Project
End-to-end Ecommerce Lakehouse ETL pipeline using Databricks, PySpark, Delta Lake, AWS S3, and Medallion Architecture.

# 🛒 Ecommerce Lakehouse Project

An end-to-end Ecommerce Lakehouse Data Engineering project built using PySpark, Databricks, Delta Lake, and AWS S3 following Medallion Architecture principles.

This project simulates a real-world batch data engineering pipeline where raw ecommerce datasets are ingested, cleaned, validated, transformed, and loaded into analytics-ready Gold tables for reporting and business intelligence.

---

# 📌 Project Overview

In this project, I built a production-style Ecommerce Lakehouse pipeline using:
<img src="./docs/project-architecture.png" alt="Project Architecture" width="400">


- PySpark
- Databricks
- Delta Lake
- AWS S3
- Databricks Workflows
- Medallion Architecture (Bronze → Silver → Gold)

The project processes multiple ecommerce datasets such as:

- Customers
- Products
- Payments
- Shipments
- Orders

The pipeline performs:
- Raw data ingestion
- Data quality validation
- Duplicate handling
- Incremental processing
- Delta MERGE upserts
- Foreign key validation
- Gold dimensional modeling
- Workflow orchestration

---

# 🏗️ Architecture

The project follows the Medallion Architecture pattern.

## 🟤 Bronze Layer
Stores raw ingested data exactly as received from source systems with minimal transformations.

### Operations Performed:
- Raw file ingestion from AWS S3
- Metadata tracking
- Schema enforcement
- Append-only ingestion
- Audit column generation

---

## ⚪ Silver Layer
Cleans and standardizes raw Bronze data into validated business-ready datasets.

### Operations Performed:
- Null validation
- Duplicate removal
- Data cleansing
- Email validation
- Price validation
- Data type standardization
- Incremental MERGE logic
- Quarantine handling for bad records
- Foreign key validation

---

## 🟡 Gold Layer
Creates analytics-ready business tables optimized for reporting and dashboards.

### Operations Performed:
- Dimensional modeling
- Fact and Dimension table creation
- Incremental upserts
- Business-ready transformations
- Reporting-friendly structure

---

# 📂 Datasets Used

| Dataset | Description |
|---|---|
| Customers | Customer profile information |
| Products | Product catalog data |
| Payments | Payment transaction details |
| Shipments | Shipment and delivery tracking |
| Orders | Ecommerce order transactions |

---

# 🧹 Data Quality Checks Implemented

This project includes several real-world data validation checks.

## ✅ Customer Checks
- Invalid email validation
- Duplicate customer handling
- Null value handling
- City standardization
- Signup date validation

## ✅ Product Checks
- Duplicate product removal
- Invalid price validation
- Product name cleanup

## ✅ Payment Checks
- Negative amount validation
- Duplicate payment handling
- Latest payment record selection

## ✅ Orders Checks
- Foreign key validation against:
  - Customers
  - Products
  - Payments
  - Shipments

## ✅ Quarantine Handling
Bad records are stored separately in quarantine tables for investigation instead of silently dropping data.

---

# 🔄 Incremental Processing

The project uses Delta Lake MERGE operations for incremental upserts.

Implemented:
- SCD Type 1 logic
- Conditional updates
- Null-safe comparisons
- Incremental inserts for new records

This avoids full table reloads and simulates real-world warehouse processing.

---

# 🧠 Key Engineering Concepts Used

- Medallion Architecture
- Delta Lake MERGE
- Incremental ETL/ELT Processing
- Fact & Dimension Modeling
- Data Validation
- Quarantine Tables
- Workflow Orchestration
- Foreign Key Validation
- Window Functions
- Duplicate Handling
- Null-safe MERGE Conditions
- Batch Processing

---

# ⚙️ Workflow Orchestration

Databricks Workflows were used to orchestrate the complete pipeline.

### Dependency Flow:
- Bronze pipelines run independently
- Silver Orders depends on:
  - Silver Customers
  - Silver Products
  - Silver Payments
  - Silver Shipments
- Gold Orders depends on:
  - Gold Customers
  - Gold Products
  - Gold Payments
  - Gold Shipments

This simulates real enterprise dependency-driven orchestration.

---

# 📊 Gold Layer Data Model

## Dimension Tables
- dim_customers
- dim_products

## Fact Tables
- fact_orders
- fact_payments
- fact_shipments

The Gold layer is designed for:
- BI reporting
- Dashboarding
- Business analytics
- KPI calculations

---

# ☁️ Technologies Used

| Technology | Purpose |
|---|---|
| PySpark | Distributed data processing |
| Databricks | Data engineering platform |
| Delta Lake | ACID transactions & MERGE |
| AWS S3 | Cloud object storage |
| SQL | Data querying |
| Databricks Workflows | Orchestration |

---

# 📁 Project Structure

```text
Ecommerce-Lakehouse-Project/
│
├── 01_setup_file/
├── 02_bronze/
├── 03_silver/
├── 04_gold/
├── orchestration/
├── README.md
