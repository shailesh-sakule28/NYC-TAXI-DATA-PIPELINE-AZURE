# 🚖 Azure Data Factory Pipeline Documentation

## NYC Taxi Data Ingestion (HTTP → ADLS Gen2)

---

## 📌 Pipeline Overview

**Pipeline Name:** `nycWebtoDL`

**Objective:**
To design a dynamic and scalable Azure Data Factory pipeline that ingests NYC Taxi Parquet files (month-wise) from an external HTTP source into Azure Data Lake Storage Gen2 using parameterized datasets and control flow logic.

---

## 🏗️ Solution Design

The pipeline leverages dynamic expressions and control flow activities to automate ingestion for all months of a given year.

---

## 🔁 ForEach Activity

### Configuration:

* **Expression:**

  ```
  @range(1,12)
  ```

* Generates a sequence of months: `1 → 12`

* **Execution Mode:**

  ```
  isSequential = true
  ```

### Purpose:

* Iterates through each month dynamically
* Ensures controlled execution to avoid throttling or overload on the source system

---

## 🔀 Conditional Logic (If Activity)

### Expression:

```
@greater(item(), 9)
```

### Purpose:

* Handles file naming differences between:

  * Single-digit months (`01–09`)
  * Double-digit months (`10–12`)

---

## 📥 Data Extraction Strategy

### 🔴 Case 1: Months 1–9

* File naming requires leading zero

* Example:

  ```
  green_tripdata_2023-01.parquet
  ```

* Implemented using dataset parameter:

  ```
  0@{dataset().p_month}
  ```

---

### 🟢 Case 2: Months 10–12

* Month value used directly
* Example:

  ```
  green_tripdata_2023-10.parquet
  ```

---

## 📦 Copy Activity Configuration

### Source:

* Type: HTTP
* Format: Parquet
* Configuration: `HttpReadSettings`
* Function: Downloads Parquet files from external source

### Sink:

* Type: Azure Data Lake Storage Gen2 (BlobFS)
* Format: Parquet
* Configuration: `AzureBlobFSWriteSettings`
* Function: Stores ingested data in Bronze layer

---

## 🔄 End-to-End Pipeline Flow

```
ForEach (1 → 12)
        ↓
   If (month > 9)
     /         \
  No           Yes
(01–09)     (10–12)
   ↓            ↓
Copy          Copy
   ↓            ↓
ADLS Gen2     ADLS Gen2
```

---

## 🧠 Key Concepts Implemented

* Dynamic iteration using `@range()`
* Conditional branching using `@greater()`
* Parameterized datasets for flexible ingestion
* Dynamic file path construction
* Batch-based ingestion design
* Integration of HTTP source with ADLS Gen2

---

## ⚡ Optimization Opportunity

The current implementation uses conditional branching to manage month formatting.
This can be simplified using the following expression:

```
@formatNumber(item(), '00')
```

### Benefits:

* Eliminates the need for:

  * If Condition activity
  * Multiple datasets
* Simplifies pipeline design
* Improves maintainability

---

## 💬 Conclusion

This pipeline demonstrates a scalable and reusable ingestion pattern using Azure Data Factory. By leveraging dynamic expressions, parameterization, and control flow, the solution efficiently automates data ingestion from an external source into Azure Data Lake, forming the foundation of a robust data engineering pipeline.

---
