# System Architecture — InsightHub

## 1. Overview
InsightHub is built as a modular, cloud-ready data intelligence platform that connects data collection, processing, analytics, and visualization in a unified workflow.  
The architecture is designed for **traceability**, **observability**, and **scalability**, ensuring every step from raw data ingestion to insight delivery is transparent and automated.

---

## 2. Core Components

### 2.1 Data Source Layer
Raw data originates from public datasets, APIs, CSV files, or internal business systems.  
These inputs represent the starting point of the InsightHub data pipeline.

### 2.2 Data Storage Layer (PostgreSQL)
A relational PostgreSQL database stores all structured information about datasets, ingestion events, and quality metrics.  
The data model follows a star-like schema centered on the `datasets` table, ensuring strong relationships between data, metrics, and operations.

### 2.3 Processing Layer (FastAPI Backend)
The backend layer is implemented with **FastAPI**, providing RESTful endpoints to access and manipulate data.  
This layer connects directly to PostgreSQL via SQLAlchemy ORM and serves as the interface between the raw data and the analytics layer.

**Responsibilities:**
- Manage CRUD operations for datasets, events, and metrics.  
- Expose endpoints for dashboards and BI tools.  
- Validate and transform incoming data.  
- Support monitoring endpoints (e.g., `/health`, `/metrics`).  

### 2.4 Analytics & Visualization Layer (Streamlit / Power BI)
This layer transforms stored data into actionable insights.  
Streamlit (or Power BI) connects to the FastAPI API or directly to PostgreSQL to display KPIs, visualizations, and trend analyses.

**Example KPIs:**
- Data freshness (SLA compliance)
- Completeness ratio
- Ingestion latency
- Error rate
- Total dataset volume

Dashboards provide a **business-friendly view** of technical metrics and data quality evolution over time.

### 2.5 Automation & Deployment Layer (Docker + CI/CD + Cloud)
InsightHub is containerized using **Docker**, allowing consistent deployment across environments.  
Automated CI/CD pipelines (via **GitHub Actions**) handle build, test, and deployment processes.  
The final deployment is hosted on **Azure App Services** and **Azure Database for PostgreSQL**, or alternatively AWS equivalents.

**Automation Goals:**
- Continuous integration of new code.  
- Continuous delivery of the latest version to production.  
- Simplified environment management (through Docker Compose).  

---

## 3. Data Flow Description

1. **Data Ingestion** — Raw datasets are fetched via ETL scripts or API connectors and stored in PostgreSQL.  
2. **Event Logging** — Each operation (ingestion, transformation, error) is logged in the `events` table.  
3. **Metric Calculation** — KPIs such as freshness and completeness are computed and stored in `metrics`.  
4. **API Exposure** — FastAPI serves endpoints to access datasets, metrics, and events.  
5. **Visualization** — The BI or frontend layer displays metrics and dataset performance through dashboards.  
6. **Automation & Monitoring** — GitHub Actions ensure continuous deployment, while metrics can be monitored through `/health` endpoints.

---

## 4. Technologies Summary

| Layer | Technology | Purpose |
|--------|-------------|----------|
| Data Storage | PostgreSQL | Structured data storage |
| Backend API | FastAPI + SQLAlchemy | RESTful data access and management |
| Analytics / Visualization | Streamlit / Power BI | KPI dashboards and BI storytelling |
| Automation / Deployment | Docker + GitHub Actions + Azure | CI/CD and cloud hosting |

---

## 5. Diagram Overview (Text Representation)

```
          ┌─────────────────────┐
          │   Data Sources       │
          │ (APIs, CSVs, etc.)  │
          └─────────┬───────────┘
                    │
                    ▼
         ┌─────────────────────┐
         │   ETL & Ingestion   │
         │ (Python / Scripts)  │
         └─────────┬───────────┘
                    │
                    ▼
         ┌─────────────────────┐
         │   PostgreSQL DB     │
         │ datasets, events,   │
         │ metrics, users      │
         └─────────┬───────────┘
                    │
                    ▼
         ┌─────────────────────┐
         │   FastAPI Backend   │
         │  REST API + ORM     │
         └─────────┬───────────┘
                    │
         ┌──────────┴──────────┐
         ▼                     ▼
┌─────────────────┐     ┌─────────────────┐
│ Streamlit / BI  │     │ Power BI        │
│ Dashboards      │     │ Visualization   │
└─────────────────┘     └─────────────────┘

                    │
                    ▼
         ┌─────────────────────┐
         │  CI/CD & Cloud      │
         │  Docker, Azure, etc.│
         └─────────────────────┘
```

---

## 6. Design Principles

- **Transparency** – Every step in the pipeline is logged and observable.  
- **Scalability** – Modular architecture allows horizontal growth (more datasets, new KPIs, new dashboards).  
- **Reproducibility** – Docker ensures identical environments for dev, test, and prod.  
- **Maintainability** – Clean API interfaces, documented flows, and automated testing.  

---

## 7. Future Enhancements

- Integrate ML-driven anomaly detection on data quality KPIs.  
- Add automated alerts for SLA violations (via email or Teams/Slack).  
- Introduce a role-based access control (RBAC) system for API endpoints.  
- Implement performance monitoring dashboards using Prometheus/Grafana.

---

## 8. Conclusion
The InsightHub architecture connects every part of the data value chain — ingestion, storage, processing, analysis, and deployment — into a single cohesive ecosystem.  
It demonstrates the full lifecycle of data in an intelligent, maintainable, and production-grade environment.
