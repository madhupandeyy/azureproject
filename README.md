# 🎵 Spotify DAB & Gold Lakeflow Pipeline 🚀

> **End-to-End Azure Data Engineering Project using Databricks Lakeflow Declarative Pipelines (Delta Live Tables), Azure Data Factory, and Medallion Architecture**

---

## 📌 Project Overview

This repository contains a **production-style Azure Data Engineering implementation** designed to demonstrate modern, scalable, and maintainable data pipelines used in real-world enterprise environments.

The project leverages **Azure services + Databricks Lakeflow Declarative Pipelines (formerly Delta Live Tables)** to build reliable data pipelines for Spotify analytics and gold-level data products.

The solution follows **Lakehouse + Medallion Architecture**:

```

Raw Data → Bronze → Silver → Gold → Analytics / BI / ML

````

### 🔹 Main Components

#### 🎧 `spotify_dab`
- Ingests raw Spotify data
- Performs cleaning and transformation
- Produces high-quality, query-ready datasets

#### 🥇 `gold_dlt_pipeline`
- Consumes cleaned datasets
- Applies business logic and aggregations
- Produces gold-level analytics tables & materialized views

Both pipelines are designed for:

- Scalability
- Modularity
- Data quality
- Maintainability
- Production readiness

---

## 🎯 Project Goals & Learning Outcomes

This project demonstrates:

- Dynamic pipelines with incremental loading & backfilling
- Azure Data Factory orchestration
- Databricks Autoloader & Spark Structured Streaming
- Bronze → Silver → Gold medallion architecture
- Slowly Changing Dimensions (SCD Type 2)
- Metadata-driven pipelines
- Data quality expectations (Lakeflow)
- Unity Catalog governance
- GitHub integration & CI/CD
- Databricks Asset Bundles deployment

This project is beginner-friendly while incorporating advanced industry concepts.

---

## 🏗️ Architecture

```mermaid
flowchart TD
A[Spotify Raw Data / Azure SQL DB] --> B[Azure Data Factory - Ingestion]
B --> C[Bronze Layer - ADLS Gen2]
C --> D[spotify_dab Pipeline]
D --> E[Silver Layer - Cleaned Data]
E --> F[gold_dlt_pipeline]
F --> G[Gold Analytics Tables & Views]
G --> H[BI / ML / Reporting]
````

### Architecture Summary

| Layer           | Technology         | Purpose                      |
| --------------- | ------------------ | ---------------------------- |
| Source          | Azure SQL Database | Cloud-hosted source data     |
| Orchestration   | Azure Data Factory | ETL pipelines & scheduling   |
| Storage         | ADLS Gen2          | Bronze, Silver, Gold layers  |
| Processing      | Azure Databricks   | Streaming + batch transforms |
| Governance      | Unity Catalog      | Metadata & access control    |
| Pipeline Engine | Lakeflow / DLT     | Declarative pipelines        |
| Version Control | GitHub             | Collaboration & CI/CD        |

---

## 🧱 Medallion Architecture

### 🥉 Bronze Layer — Raw Data

* Ingestion from Azure SQL Database
* Dynamic pipelines with parameterized queries
* JSON watermark management for incremental loads
* Backfill support
* Raw storage in Delta/Parquet format

---

### 🥈 Silver Layer — Enriched Data

* Databricks Autoloader for streaming ingestion
* Schema evolution support
* Data cleansing & standardization
* Deduplication
* Modular PySpark transformations

---

### 🥇 Gold Layer — Curated Analytics

* Built with Lakeflow Declarative Pipelines
* Aggregations and business logic
* Materialized views
* Slowly Changing Dimensions (SCD Type 2)
* Data quality expectations

---

## 📂 Repository Structure

```
/
├── spotify_dab/
│   ├── notebooks/
│   ├── pipeline/
│   └── README.md
│
├── gold_dlt_pipeline/
│   ├── notebooks/
│   ├── pipeline/
│   └── README.md
│
├── docs/
│   └── architecture.md
│
├── .github/
│   └── workflows/
│       └── sync_git_folder.yml
│
├── requirements.txt
└── README.md
```

### Folder Explanation

* **notebooks/** → Interactive development and testing
* **pipeline/** → Lakeflow pipeline source code (Python/SQL)
* **docs/** → Architecture and documentation
* **.github/** → CI/CD workflows

---

## ⚙️ End-to-End Pipeline Flow

### 1️⃣ Azure Resource Setup

* Azure SQL Database (source)
* Azure Data Factory
* Azure Data Lake Storage Gen2
* Azure Databricks Workspace
* Unity Catalog & External Locations
* Access Connectors & Credentials

---

### 2️⃣ Bronze Layer — Data Ingestion (ADF)

Implemented using Azure Data Factory activities:

* Lookup
* Copy
* If Condition
* Delete
* Script

#### Features

* Incremental loading using CDC timestamps
* JSON watermark files
* Dynamic SQL query generation
* Conditional logic to avoid empty files
* Historical data backfill support

---

### 3️⃣ Silver Layer — Databricks Transformations

* Spark Structured Streaming
* Auto Loader incremental ingestion
* Streaming writes to Delta tables

Example transformations:

* Case-when columns
* Regex replacements
* Deduplication
* Type normalization
* Schema evolution

---

### 4️⃣ Gold Layer — Lakeflow Declarative Pipelines

Built using Delta Live Tables:

* Materialized views
* Aggregated analytics datasets
* SCD Type 2 implementation
* Auto CDC workflows
* Data lineage and expectations

---

## 🔄 Incremental Pipeline Design

Key strategy:

* Store last CDC timestamps in JSON files
* Dynamically generate SQL queries
* Parameterized pipeline execution
* Optional backfilling using `from_date`

Benefits:

* Efficient data loads
* Reduced compute costs
* Highly reusable pipelines

---

## 🧩 Metadata-Driven Development

Dynamic SQL generation using **Ginja templating**:

* Parameterized joins
* Reusable business views
* Reduced hardcoding
* Easier scaling and maintenance

---

## 🔥 Lakeflow Pipeline Details

### 🎧 spotify_dab Pipeline

**Purpose**

* Ingest and transform raw Spotify datasets.

**Key Features**

* Streaming ingestion via Auto Loader
* Schema evolution
* Modular transformations
* Data quality enforcement

---

### 🥇 gold_dlt_pipeline

**Purpose**

* Generate analytics-ready gold datasets.

**Key Features**

* Aggregations (Top artists, most played tracks)
* Materialized views
* SCD Type 2 historical tracking
* Business logic constraints

---

## 🚀 Getting Started

### 1️⃣ Clone Repository

```bash
git clone https://github.com/madhupandeyy/azureproject.git
```

---

### 2️⃣ Import Into Databricks

1. Open Databricks Workspace
2. Right-click user folder → **Create > Git Folder**
3. Paste repository URL
4. Authenticate with GitHub

---

### 3️⃣ Install Dependencies

```bash
pip install -r requirements.txt
```

---

### 4️⃣ Configure & Run Pipelines

In Databricks:

* Configure storage locations
* Select compute (Serverless or Classic)
* Set target schema
* Start pipeline execution

---

## 🔄 Development & Git Integration

Recommended workflow:

1. Create feature branch
2. Develop notebooks/pipelines
3. Commit & push changes
4. Create Pull Request
5. Merge into main

### CI/CD

Workflow:

```
.github/workflows/sync_git_folder.yml
```

Automates:

* Databricks Git sync
* Deployment flow
* Environment consistency

---

## 📦 Databricks Asset Bundles (CI/CD)

Used for deploying:

* Notebooks
* Workflows
* Configuration YAML files

Typical commands:

```bash
bundle validate
bundle summary
bundle deploy --target dev
```

---

## 🔔 Monitoring & Alerts

Pipeline monitoring implemented using:

* Azure Logic Apps
* ADF Web Activity
* Webhook-based email alerts

Triggers automatic notifications on failures.

---

## 🌟 Best Practices Implemented

* Modular pipeline architecture
* Metadata-driven transformations
* Data quality expectations
* Idempotent streaming writes
* Secure credential management
* Clean Git branching strategy
* Reusable Python utilities

---

## 📚 Key Concepts & Definitions

| Concept                | Description                               |
| ---------------------- | ----------------------------------------- |
| Medallion Architecture | Bronze → Silver → Gold data layering      |
| Incremental Load       | Load only new/changed data                |
| Backfilling            | Reload historical datasets                |
| Autoloader             | Streaming ingestion with schema evolution |
| Delta Live Tables      | Declarative data pipelines                |
| SCD Type 2             | Historical version tracking               |
| Unity Catalog          | Central metadata governance               |
| Asset Bundles          | CI/CD deployment packaging                |

---

## 🧪 Example Analytics Use Cases

* Top artists analysis
* Most played tracks
* User listening trends
* Historical playback insights
* Streaming analytics reporting

---

## 🤝 Contributing

Contributions are welcome!

Steps:

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Open a Pull Request

---

## ⭐ Portfolio Note

This project demonstrates:

✔ End-to-end Azure Data Engineering
✔ Lakehouse + Medallion implementation
✔ Streaming + Batch pipelines
✔ CI/CD integration
✔ Production-grade data architecture

If you found this project useful, consider giving it a ⭐ on GitHub!
