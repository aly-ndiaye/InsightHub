# Vision & KPIs — InsightHub

## 1. Analytical Vision
InsightHub aims to transform raw operational data into measurable intelligence through automated data collection, performance tracking, and storytelling dashboards.  
The platform focuses on **data observability**, ensuring that every dataset is measurable, traceable, and optimized for decision-making.

By integrating data engineering and business intelligence, InsightHub provides real-time visibility into the quality and reliability of data pipelines.

---

## 2. Business Use Case
The primary use case is **data quality and pipeline monitoring**.  
For each dataset ingested or updated, the system logs operational events and calculates quality metrics to assess freshness, completeness, latency, and reliability over time.

Decision-makers can identify which datasets are healthy, which need intervention, and how overall data reliability evolves across the organization.

---

## 3. Key Performance Indicators (KPIs)

### 3.1 Data Freshness
**Definition:** Measures how up-to-date each dataset is relative to its expected update frequency.  
**Formula:** `freshness = 1 - (days_since_last_update / SLA_days)`  
**Goal:** Maintain 90%+ of datasets updated within SLA (Service Level Agreement).  
**Value:** Indicates how reactive and reliable the pipeline is.

---

### 3.2 Data Completeness
**Definition:** Percentage of non-null or valid records in each dataset.  
**Formula:** `completeness = (valid_records / total_records)`  
**Goal:** > 95% completeness for critical datasets.  
**Value:** Evaluates whether datasets are usable for analysis and machine learning.

---

### 3.3 Ingestion Latency
**Definition:** Time between the start of data ingestion and successful load into PostgreSQL.  
**Formula:** `latency = end_time - start_time`  
**Goal:** Average latency below 10 seconds for small datasets.  
**Value:** Monitors technical efficiency and scalability of ETL processes.

---

### 3.4 Error Rate
**Definition:** Percentage of ingestion or transformation operations that failed.  
**Formula:** `error_rate = failed_operations / total_operations`  
**Goal:** Error rate below 5%.  
**Value:** Measures system stability and identifies datasets that frequently fail.

---

### 3.5 Dataset Volume
**Definition:** Total number of rows stored for each dataset over time.  
**Formula:** `record_count = COUNT(*)`  
**Goal:** Continuous tracking of data growth and ingestion throughput.  
**Value:** Monitors pipeline performance and helps detect unexpected drops or spikes.

---

### 3.6 SLA Compliance
**Definition:** Percentage of datasets meeting their freshness and latency targets.  
**Formula:** `sla_compliance = datasets_meeting_sla / total_datasets`  
**Goal:** SLA compliance above 90%.  
**Value:** Global indicator of pipeline health and reliability.

---

## 4. Monitoring Strategy
Each metric will be computed automatically during the ETL pipeline execution and stored in the `metrics` table with timestamps.  
Dashboards in Streamlit or Power BI will visualize these metrics through time series, allowing users to monitor trends, compare datasets, and receive alerts when thresholds are breached.

---

## 5. Visualization Examples
- Line chart: Data freshness evolution per dataset over time.  
- Bar chart: Error rate comparison by dataset.  
- KPI cards: Completeness %, Average latency, SLA compliance.  
- Table view: Latest metrics and dataset statuses.  

---

## 6. Strategic Value
Tracking these KPIs enables InsightHub to:
- Ensure **data trust and reliability**.  
- Detect pipeline issues proactively.  
- Provide **transparency** on data lifecycle health.  
- Align data operations with business SLAs.  

By turning these metrics into actionable insights, InsightHub evolves from a simple monitoring system into a **decision intelligence platform**.
