# Healthcare Data Engineering Pipeline: Medallion Architecture

## 📌 Project Overview
This project is an end-to-end **Delta Live Tables (DLT)** data pipeline built for healthcare data processing. It implements a production-ready **Bronze-Silver-Gold medallion architecture** using PySpark. The pipeline seamlessly ingests real-time streaming patient data, enforces strict data quality constraints, and models the data for multi-dimensional business analytics.

##  Tech Stack
* **Language:** Python / PySpark
* **Framework:** Databricks Delta Live Tables (DLT)
* **Architecture:** Medallion (Bronze, Silver, Gold)
* **Cloud Infrastructure:** Google Cloud Platform (GCS, Compute Engine)
* **Key Features:** Streaming data ingestion, automated data quality (EXPECT constraints), Schema Evolution

##  Architecture Design

    <img width="2590" height="3566" alt="image" src="https://github.com/user-attachments/assets/f63a238b-c15f-44a4-889b-5a3981ec6601" />

*The pipeline processes raw daily admission records and reference mapping files through three distinct layers.*

### 1. Bronze Layer (Raw & Streaming Ingestion)
* Ingests real-time patient admission data (`STREAM()`) and batch reference mapping tables.
* **Data Quality:** Drops records missing critical primary keys (e.g., `patient_id`) before they enter the data lake.

### 2. Silver Layer (Enrichment & Business Logic)
* Merges streaming patient data with diagnostic reference mapping.
* Applies dynamic COALESCE logic for unmapped codes and enforces constraints to ensure all downstream records have valid diagnostic descriptions.

### 3. Gold Layer (Aggregated Analytics)
* Produces clean, business-ready Live Tables optimized for hospital operations and research.
* **Outputs:** Daily operational metrics (capacity planning), demographic analysis, and diagnostic trends.

## 📁 Repository Structure
```text
├── src/
│   └── healthcare_dlt_processing.py    # Complete PySpark Medallion pipeline (Bronze, Silver, Gold)
├── data/                               # Sample raw CSV files for testing
└── README.md
