# Healthcare Data Engineering Pipeline: Medallion Architecture

## 📌 Project Overview
This project is an end-to-end data pipeline built for healthcare data processing. It implements a production-ready **Bronze-Silver-Gold medallion architecture**. The project utilizes PySpark for automated raw data ingestion from Unity Catalog Volumes, and Databricks SQL via Delta Live Tables (DLT) for streaming data quality enforcement and multi-dimensional analytics.

## 🛠️ Tech Stack
* **Languages:** Python (PySpark), Databricks SQL
* **Framework:** Databricks Delta Live Tables (DLT)
* **Storage & Governance:** Delta Lake, Unity Catalog Volumes
* **Architecture:** Medallion (Bronze, Silver, Gold)

## 🏗️ Architecture Design

```mermaid
graph TD
    subgraph Unity Catalog Volumes
        A[patients_daily_file.csv <br> Daily Append]:::raw
        B[diagnosis_mapping.csv <br> Batch]:::raw
    end

    subgraph PySpark Ingestion 
        C[(Delta Tables <br> raw_patients_daily)]:::pyspark
    end

    subgraph DLT Pipeline (Databricks SQL)
        D[(Bronze Layer <br> Streaming Ingestion)]:::bronze
        E[(Silver Layer <br> Enriched & Cleaned)]:::silver
        F[(Gold Layer <br> Business Analytics)]:::gold
    end

    A -->|PySpark Read| C
    B -->|PySpark Read| C
    C -->|STREAM| D
    D -->|DQ Checks & LEFT JOIN| E
    E -->|Aggregations| F

    classDef raw fill:#f9f9f9,stroke:#333,stroke-width:2px;
    classDef pyspark fill:#00599C,stroke:#333,stroke-width:2px,color:#fff;
    classDef bronze fill:#cd7f32,stroke:#333,stroke-width:2px,color:#fff;
    classDef silver fill:#c0c0c0,stroke:#333,stroke-width:2px;
    classDef gold fill:#ffd700,stroke:#333,stroke-width:2px;
