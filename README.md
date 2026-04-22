# 🚖 NYC Taxi Data Pipeline on Azure (ADF | Databricks | Medallion Architecture)

## 📌 Overview

This project implements an end-to-end, production-style batch data engineering pipeline on Azure using the NYC Taxi dataset. The solution follows a **Medallion Architecture (Bronze, Silver, Gold)** to enable scalable, maintainable, and analytics-ready data processing.

The pipeline ingests raw data, processes it using distributed compute in Databricks, and delivers curated datasets for business intelligence and analytics.

---

## ⚡ Key Highlights (Quick Summary)

- Built end-to-end batch data pipeline on Azure using ADF and Databricks  
- Implemented Medallion Architecture (Bronze → Silver → Gold)  
- Designed scalable ingestion using parameterized ADF pipelines  
- Performed distributed data processing using PySpark  
- Delivered analytics-ready datasets for business reporting and decision-making  

---

## 🏗️ Architecture

![Architecture Diagram](./docs/data_architecture.png)

---

## 🔄 End-to-End Data Flow

**Source → ADF Ingestion → Bronze → Databricks Transformation → Silver → Gold → Consumption**

---

## 📁 Repository Structure

- `docs/` → Architecture diagrams and documentation  
- `notebooks/` → Databricks notebooks (Bronze, Silver, Gold transformations)  
- `README.md` → Project overview and documentation  

---

## 🔹 Data Source

- Dataset: NYC Taxi Data  
- Format: Parquet Files  
- Access Method: HTTPS  

---

## 🥉 Bronze Layer – Raw Data Ingestion

### Tool: Azure Data Factory (ADF)

A dynamic and parameterized ingestion pipeline is implemented to fetch data from external sources.

### Key Features:

- Parameterized pipelines for flexible ingestion (dataset type, date ranges)  
- Scalable design to support multiple datasets  
- Automated ingestion using ADF activities  

### Details:

- Load Type: Batch Processing  
- Load Strategy: Full Load (parameter-driven ingestion)  
- Write Mode: Append  
- Transformations: None  
- Storage: Azure Data Lake Storage Gen2  

### Purpose:

- Preserve raw data in original format  
- Enable reprocessing and auditing  

---

## 🥈 Silver Layer – Data Transformation

### Tool: Azure Databricks (PySpark)

Raw data is transformed into clean, structured datasets.

### Transformations:

- Data cleansing and validation  
- Schema enforcement  
- Handling null/missing values  
- Deduplication  
- Data standardization  
- Derived columns  

### Details:

- Load Type: Batch Processing  
- Load Strategy: Full Load  
- Write Mode: Overwrite  
- Output: Cleaned structured datasets  

### Purpose:

- Improve data quality  
- Create consistent datasets for downstream use  

---

## 🥇 Gold Layer – Business & Analytics Layer

### Tool: Azure Databricks (SQL / PySpark)

The Gold layer produces business-ready datasets optimized for analytics.

### Transformations:

- Data integration across datasets  
- Aggregations (trip counts, revenue metrics)  
- Business logic implementation  
- KPI calculations  

### Data Modeling:

- Star schema (Fact & Dimension tables)  
- Aggregated datasets  
- Denormalized structures for performance  

### Purpose:

- Enable fast analytical queries  
- Deliver curated datasets for reporting and decision-making  

---

## 📊 Data Consumption

The Gold layer supports:

- Business Intelligence dashboards  
- Ad-hoc SQL queries  
- Analytical use cases  

---

## ⚙️ Technologies Used

- Azure Data Factory (ADF)  
- Azure Data Lake Storage Gen2  
- Azure Databricks  
- PySpark  
- Parquet  
- Delta Lake  

---

## 🔐 Security & Authentication

Secure access is implemented using a **Service Principal via Microsoft Entra ID (Azure AD)**.

### Implementation:

- Created Service Principal (App Registration)  
- Configured Client ID and Secret  
- Assigned **Storage Blob Data Contributor** role  
- Enabled secure access using ABFSS protocol  

### Best Practices:

- Secrets should be stored using:
  - Azure Key Vault  
  - Databricks Secret Scope  

---

## 🚀 Key Highlights (Technical)

- Dynamic and parameterized ingestion pipelines in ADF  
- End-to-end pipeline from ingestion to analytics  
- Implementation of Medallion Architecture  
- Scalable and modular pipeline design  
- Secure authentication using Service Principal  

---

## 📈 Future Enhancements

- Implement incremental (delta) loading  
- Extend Delta Lake usage across layers  
- Add orchestration triggers and monitoring  
- Integrate Power BI dashboards  
- Implement CI/CD for pipeline deployment  

---

## 💬 Conclusion

This project demonstrates how to design and implement a scalable, secure, and production-ready data engineering pipeline on Azure. It highlights best practices in data ingestion, transformation, modeling, and security.

---

## 👨‍💻 Author

**Shailesh Sakule**
