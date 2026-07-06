# Databricks Unified Lakehouse Pipeline

## 📌 Project Overview
This project demonstrates the creation of a multi-hop Data Lakehouse architecture (Medallion Architecture) using Databricks. It features a complete ETL/ELT pipeline that ingests real-time streaming data, processes it through Bronze, Silver, and Gold layers, and applies advanced Delta Lake optimizations and data governance rules.

## 🛠️ Tech Stack
* **Platform:** Databricks (Serverless Free Edition / Unity Catalog)
* **Languages:** Python (PySpark), SQL
* **Libraries:** `Faker`
* **Storage:** Delta Lake

## 🚀 Key Features Implemented

1. **3-Tier Architecture & Data Modeling:** * Designed a 5-table schema across `bronze_layer`, `silver_layer`, and `gold_layer`.
2. **Spark Structured Streaming:** * Integrated the `Faker` library using PySpark UDFs to generate and ingest realistic driver data continuously.
3. **Fault Tolerance:** * Implemented streaming state recovery using Databricks Volumes for `checkpointLocation`.
4. **Delta Lake Internals:** * **Schema Evolution:** Dynamically added a `phone` column to the live stream using `.option("mergeSchema", "true")`.
   * **Time Travel & Recovery:** Demonstrated the ability to query previous table states and use the `RESTORE` command to roll back unwanted schema changes.
5. **Advanced Performance Tuning:** * **Z-Ordering:** Applied to the Silver layer (`drivers_clean`) to physically optimize file layout for high-cardinality queries.
   * **Liquid Clustering:** Applied to the Gold layer (`drivers_active`) for dynamic data layout and flexibility.
6. **Data Governance (DCL):** * Configured Unity Catalog permissions using `GRANT` and `REVOKE` syntax to strictly control `SELECT` and `MODIFY` privileges on Gold layer tables.

## ⚠️ Notes for Mentor regarding Environment Limitations
This pipeline was developed using the Databricks Serverless Free Edition. Due to the restricted nature of the free tier:
* **Governance:** Account-level group creation is disabled. Therefore, `GRANT` and `REVOKE` statements were applied directly to the authorized workspace user to demonstrate correct Unity Catalog syntax, rather than a mocked group.
* **Legacy Commands:** Unity Catalog relies on a "Secure by Default" model and does not support the legacy `DENY` command. The modern `REVOKE` command was used to satisfy the restriction requirement.
