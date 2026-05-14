# Healthcare Data Engineering Pipeline: Medallion Architecture

## 📌 Project Overview
This project is an end-to-end data pipeline built for healthcare data processing. It implements a production-ready **Bronze-Silver-Gold medallion architecture**. The project utilizes PySpark for automated raw data ingestion from Unity Catalog Volumes, and Databricks SQL via Delta Live Tables (DLT) for streaming data quality enforcement and multi-dimensional analytics.

## 🛠️ Tech Stack
* **Languages:** Python (PySpark), Databricks SQL
* **Cloud Platform:** Google Cloud Platform (GCS, Compute Engine)
* **Framework:** Databricks Delta Live Tables (DLT)
* **Storage & Governance:** Delta Lake, Unity Catalog Volumes
* **Architecture:** Medallion (Bronze, Silver, Gold)

## 🏗️ Pipeline Architecture Steps

### 1. Raw Ingestion (PySpark & Unity Catalog)
* Automated PySpark script reads raw CSV files directly from Databricks Unity Catalog Volumes.
* Applies explicit data type casting (e.g., String to Date) and writes to foundational Delta tables using `mergeSchema` to handle upstream schema drift.

### 2. Bronze Layer (DLT Streaming)
* Ingests real-time patient admission data (`STREAM()`) and batch reference mapping tables.
* **Data Quality:** Drops records missing critical primary keys before they enter the data lake.

### 3. Silver Layer (Enrichment & Business Logic)
* Merges streaming patient data with diagnostic reference mapping.

### 4. Gold Layer (Aggregated Analytics)
* Produces clean, business-ready Live Tables optimized for hospital operations and research.
* **Outputs:** Daily operational metrics (capacity planning), demographic analysis, and diagnostic trends.

## 📁 Repository Structure
```text
├── src/
│   ├── feed_raw_tables.ipynb           # PySpark ingestion from Unity Catalog Volumes
│   └── healthcare_dlt_processing.ipynb # Databricks SQL Medallion pipeline (Bronze, Silver, Gold)
├── data/                               # Sample raw CSV files for testing
└── README.md
