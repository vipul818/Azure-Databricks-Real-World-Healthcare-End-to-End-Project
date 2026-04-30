# 🏥 Azure Databricks Healthcare Data Engineering Project

End-to-End Real-World Data Engineering Pipeline built using Azure Databricks, ADLS Gen2, Unity Catalog, and Delta Lake to analyze hospital re-admissions.

---

## 🚀 Project Overview

This project simulates a real-world healthcare use case where a hospital network aims to reduce **30-day patient re-admissions**.

The solution ingests raw healthcare data, processes it through a **Medallion Architecture (Bronze → Silver → Gold)**, and delivers actionable insights via dashboards and AI-powered analytics.

---

## 🎯 Business Problem

A hospital network (AEX Health Hospitals) faces high **30-day re-admission rates**, leading to:

- Financial losses (non-reimbursable cases)
- Resource constraints (bed shortages)
- Poor patient experience

---

## 🎯 Objectives

- Identify diseases driving re-admissions
- Compare hospital & doctor performance
- Track 30-day re-admitted patients
- Generate cost and KPI insights

---

## 🧱 Architecture



### 📌 Medallion Architecture


---

## ⚙️ Tech Stack

- Azure Databricks
- ADLS Gen2
- Unity Catalog
- Delta Lake
- PySpark
- Databricks Autoloader
- GitHub Actions (CI/CD)
- Databricks Asset Bundles
- Lakeflow Jobs
- Genie AI
- AIBI Dashboard

---

## 🏗️ Data Model (Star Schema)

| Table | Description |
|------|------------|
| dim_patient | Patient details |
| dim_hospital | Hospital info |
| dim_diagnosis | Diagnosis data |
| fact_visit | Patient visit records |

---

## 📥 Data Ingestion (Bronze Layer)

- Source: CSV files from ADLS (`staging/`)
- Tool: **Autoloader (cloudFiles)**
- Mode: Incremental ingestion

### Key Features:
- Schema evolution
- Checkpointing
- File event-based ingestion

### Tables:
- `healthcare.bronze.patient_raw`
- `healthcare.bronze.hospital_raw`
- `healthcare.bronze.diagnosis_raw`
- `healthcare.bronze.visit_raw`

📸 _Add Screenshot: Bronze tables / Autoloader config_

---

## 🔄 Data Transformation (Silver Layer)

- Deduplication using `dropDuplicates()`
- Upsert using `DeltaTable.merge()`
- Streaming reads (`readStream`)

### Tables:
- `dim_patient`
- `dim_hospital`
- `dim_diagnosis`
- `fact_visit`

📸 _Add Screenshot: Merge logic / Silver tables_

---

## 📊 Business Layer (Gold)

### Logic:
- Window function (`lag`) for re-admission detection
- 30-day condition applied
- KPI aggregation

### Output Table:
- `healthcare.gold.hospital_diagnosis_kpi`

### KPIs:
- Re-admission rate
- Total visits
- Average cost
- Total cost

📸 _Add Screenshot: Gold table / query result_

---

## 🔁 Orchestration (Lakeflow Jobs)

- Bronze → Silver → Gold dependency pipeline
- Parallel ingestion for Bronze
- Serverless compute used

📸 _Add Screenshot: Job DAG_

---

## 📦 CI/CD (GitHub Actions + DAB)

### Workflow:

- `dev` → deploy to Dev
- `main` → deploy to Prod

### Tools:
- Databricks Asset Bundles (IaC)
- GitHub Actions

📸 _Add Screenshot: GitHub Actions run_

---

## 🧠 AI Analytics (Genie)

- Natural language queries
- SQL auto-generated

### Example Queries:
- "Hospitals with >20% re-admission rate"
- "Average stay for heart failure patients"

📸 _Add Screenshot: Genie responses_

---

## 📈 Dashboard (AIBI)

- Built-in Databricks visualization
- AI-generated charts

### Visuals:
- Visits by hospital
- Re-admission trends
- Cost analysis

📸 _Add Screenshot: Dashboard_

---

## 🔐 Unity Catalog Setup

- Catalog: `healthcare`
- Schemas: `bronze`, `silver`, `gold`
- External Locations configured for ADLS

---


## 🧪 Key Learnings

- Incremental processing with Autoloader
- Merge strategy for SCD handling
- Medallion architecture debugging
- CI/CD for data pipelines
- Unity Catalog governance

---

## 📌 How to Run

1. Upload CSV files to ADLS (`staging/`)
2. Run Lakeflow Job OR:
   - Bronze notebooks
   - Silver notebooks
   - Gold notebook
3. Query Gold table / use dashboard

---

## 📂 Project Structure

```
healthcare-data-engineering-project/
│
├── notebooks/
│   ├── bronze/
│   │   ├── diagnosis_raw_ingestion.py
│   │   ├── hospital_raw_ingestion.py
│   │   ├── patient_raw_ingestion.py
│   │   └── visit_raw_ingestion.py
│   │
│   ├── silver/
│   │   ├── dim_diagnosis_ingestion.py
│   │   ├── dim_hospital_ingestion.py
│   │   ├── dim_patient_ingestion.py
│   │   └── fact_visit_ingestion.py
│   │
│   └── gold/
│       └── readmission_analysis.py
│
├── resources/
│   └── job.yml
│
├── .github/
│   └── workflows/
│       ├── deploy-dev.yml
│       └── deploy-prod.yml
│
├── databricks.yml
├── README.md
├── requirements.txt
│
└── docs/
    ├── architecture.png
    ├── bronze_layer.png
    ├── silver_layer.png
    ├── gold_layer.png
    ├── job_pipeline.png
    ├── genie_ai.png
    └── dashboard.png
```


---

## 👨‍💻 Author

**Vipul Anand**
