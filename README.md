# Adventure Works: End-to-End Azure Data Engineering Pipeline

This project implements a scalable, dynamic data lakehouse architecture using the Azure Stack. It automates the ingestion, transformation, and serving of the Adventure Works dataset—moving data from raw API endpoints to a structured Gold layer ready for BI reporting.

## 🛠 Tech Stack
Orchestration: Azure Data Factory (ADF)

Storage: Azure Data Lake Storage (ADLS) Gen2

Compute: Azure Databricks (PySpark)

Data Warehouse: Azure Synapse Analytics

Security: Azure Key Vault & Service Principals

Format: CSV (Bronze), Parquet (Silver/Gold)

## 🏗 Architecture Overview
The project follows the Medallion Architecture to ensure data quality and lineage:

Ingestion (Bronze Layer):

Dynamic ADF pipelines pull data from the GitHub API.

Incremental Loading logic ensures only new or updated records are processed, reducing compute costs.

Data is stored in its raw format (CSV) in the bronze container.

Transformation (Silver Layer):

Databricks connects to ADLS Gen2 via a Service Principal for secure, high-performance access.

PySpark scripts handle data cleaning, schema enforcement, and type casting.

Processed data is written to the silver container in Parquet format for optimized storage and query performance.

Serving (Gold Layer / Lakehouse):

Synapse Serverless SQL: Created a Lakehouse views layer that directly reads from the Silver Parquet files.

External Tables: Persisted data into a gold container as External Tables to provide a unified platform for both Data Discovery and BI Reporting.

## 🚀 Key Features
1. Dynamic & Parameterized Pipelines
Instead of creating separate pipelines for every table, I utilized ADF Parameters and Variables. This allows a single pipeline to handle multiple tables dynamically, making the solution highly maintainable and scalable.

2. Incremental Data Loading
Implemented a "Watermark" logic within ADF to track the last loaded record. This ensures that the pipeline only fetches "Delta" changes from the GitHub API rather than performing a full reload every time.

3. Secure Unified Access
Configured Azure Service Principals and Key Vault to manage secrets. This avoids hardcoding credentials in Databricks notebooks and ensures follow-through on enterprise-grade security practices.

<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/a41b8ff5-741d-466e-bc56-8bb73862a4be" />
