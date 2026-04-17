# 📊 Microsoft Fabric — End-to-End Sales Analytics Platform

> A modern, cloud-native analytics solution built on **Microsoft Fabric**, delivering automated data pipelines, scalable Lakehouse storage, and real-time Power BI dashboards for sales intelligence and KPI monitoring.

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Business Objective](#-business-objective)
- [Architecture](#-architecture)
- [Tech Stack](#-tech-stack)
- [Medallion Architecture](#-medallion-architecture)
- [Dashboard & KPIs](#-dashboard--kpis)
- [Key Features](#-key-features)
- [Insights Generated](#-insights-generated)
- [Business Impact](#-business-impact)
- [Getting Started](#-getting-started)
- [Future Enhancements](#-future-enhancements)

---

## 📖 Overview

This project demonstrates a production-grade, **end-to-end data analytics platform** using Microsoft Fabric — covering ingestion, transformation, semantic modeling, and visualization across a unified SaaS environment.

The platform consolidates fragmented sales data into a single source of truth, enabling stakeholders to monitor KPIs, track revenue trends, and make faster data-driven decisions — all with automated pipelines and near real-time refresh.

---

## 🎯 Business Objective

| Goal | Description |
|---|---|
| **Centralize** | Single analytics platform replacing siloed, manual reports |
| **Automate** | End-to-end pipeline — zero manual data movement |
| **Accelerate** | Near real-time insights for faster stakeholder decisions |
| **Scale** | Reusable, layered architecture that grows with data volume |

---

## 🏗️ Architecture

```
┌──────────────────────────────────┐
│   Data Sources                   │
│   CSV Files · SQL DB · APIs      │
└──────────────┬───────────────────┘
               │
               ▼
┌──────────────────────────────────┐
│   Data Factory (Pipelines)       │
│   Orchestration & Ingestion      │
└──────────────┬───────────────────┘
               │
               ▼
┌──────────────────────────────────┐
│   Lakehouse — 🟤 Bronze Layer    │
│   Raw Delta Tables (As-Is)       │
└──────────────┬───────────────────┘
               │
               ▼
┌──────────────────────────────────┐
│   Transformation                 │
│   Notebooks (PySpark / SQL)      │
└──────────────┬───────────────────┘
               │
               ▼
┌──────────────────────────────────┐
│   Lakehouse — ⚪ Silver Layer    │
│   Cleaned & Structured Tables    │
└──────────────┬───────────────────┘
               │
               ▼
┌──────────────────────────────────┐
│   Semantic Model — 🟡 Gold Layer │
│   Star Schema · DAX Measures     │
└──────────────┬───────────────────┘
               │
               ▼
┌──────────────────────────────────┐
│   Power BI Dashboard             │
│   KPIs · Trends · Drill-throughs │
└──────────────────────────────────┘
```

---

## 🛠️ Tech Stack

| Component | Technology |
|---|---|
| **Cloud Platform** | Microsoft Fabric |
| **Orchestration** | Data Factory (Pipelines) |
| **Storage** | Lakehouse (Delta Tables / OneLake) |
| **Transformation** | SQL · Python / PySpark (Notebooks) |
| **Semantic Layer** | Fabric Semantic Model (Power BI Dataset) |
| **Visualization** | Power BI |
| **Data Format** | Delta Lake (Parquet + transaction log) |

---

## 🔄 Medallion Architecture

The pipeline follows the industry-standard **Bronze → Silver → Gold** medallion pattern for progressive data refinement.

### 🟤 Bronze Layer — Raw Ingestion

- Ingested raw data from multiple sources:
  - Flat files (CSV / Excel)
  - SQL databases
  - REST APIs
- Stored in **Lakehouse as Delta tables** with no transformations applied
- Full historical data preserved for auditability and reprocessing

### ⚪ Silver Layer — Cleansed & Structured

Applied business-ready transformations:

| Transformation | Detail |
|---|---|
| Null handling | Dropped or imputed missing values |
| Deduplication | Removed duplicate records by key |
| Format standardization | Dates, currency, category codes normalized |
| Business rules | Applied domain-specific filtering and flags |

**Output Tables:**

```
silver_sales
silver_customers
silver_products
```

### 🟡 Gold Layer — Semantic / Business Model

Designed a **star schema** optimized for Power BI reporting:

```
                  ┌─────────────┐
                  │  dim_Date   │
                  └──────┬──────┘
                         │
┌──────────────┐   ┌─────▼──────┐   ┌───────────────┐
│ dim_Customer ├───►  fact_Sales ◄───┤  dim_Product  │
└──────────────┘   └─────┬──────┘   └───────────────┘
                         │
                  ┌──────▼──────┐
                  │  dim_Region │
                  └─────────────┘
```

- Calculated columns for derived business fields
- DAX measures for KPI computation
- Optimized relationships for cross-filter performance

---

## 📊 Dashboard & KPIs

### Core KPIs

| KPI | Description |
|---|---|
| **Total Sales** | Gross revenue across all regions and categories |
| **Revenue Growth (MoM)** | Month-over-month % change in revenue |
| **Revenue Growth (YoY)** | Year-over-year % change in revenue |
| **Order Volume** | Total number of orders in the selected period |
| **Category Performance** | Revenue and volume broken down by product category |
| **Profitability Metrics** | Gross margin and profit contribution by segment |

### Visualizations

| Visual | Purpose |
|---|---|
| KPI Cards | At-a-glance performance snapshot |
| Line / Area Charts | Monthly and weekly revenue trends |
| Bar / Column Charts | Category-wise and region-wise sales breakdown |
| Map Visual | Geographic sales distribution |
| Top-N Table | Highest-performing products with rank |
| Drill-through Pages | Deep-dive by product, region, or customer segment |

---

## ✅ Key Features

- 🔁 **Fully automated pipeline** — Data Factory orchestrates ingestion to reporting end-to-end
- 🏛️ **Medallion Lakehouse architecture** — scalable, layered, and reprocessable
- ⭐ **Star schema semantic model** — optimized for fast DAX queries and Power BI performance
- 📊 **Interactive dashboards** — with drill-throughs, slicers, and cross-filtering
- ⚡ **Near real-time refresh** — scheduled pipeline triggers keep dashboards current
- ♻️ **Reusable pipeline components** — parameterized notebooks and pipelines for new data sources

---

## 🔍 Insights Generated

- 📦 Identified **top-performing product categories** driving the majority of revenue
- 📅 Analyzed **seasonal sales trends** and demand cycles for inventory planning
- 🌍 Detected **underperforming regions and SKUs** for targeted intervention
- 💰 Enabled **better pricing decisions** through margin and profitability visibility
- 👥 Surfaced **customer concentration risk** — high dependency on few key accounts

---

## 💼 Business Impact

| Outcome | Magnitude |
|---|---|
| Reduced manual reporting effort | ~60% reduction |
| Improved reporting accuracy | Single source of truth, no reconciliation |
| Time to insight | Near real-time vs. previous day/week lag |
| Decision-making speed | Significantly accelerated with self-serve dashboards |

---

## 🚀 Getting Started

### Prerequisites

- Microsoft Fabric workspace (Trial or paid capacity)
- Power BI Pro or Fabric license for report sharing
- Source data access (CSV / SQL / API credentials)

### Setup Steps

**1. Workspace Setup**
```
Microsoft Fabric Portal → Create Workspace → Assign Fabric Capacity
```

**2. Lakehouse Creation**
```
Workspace → New → Lakehouse → Name: sales_lakehouse
```

**3. Data Ingestion (Bronze)**
```
Workspace → New → Data Pipeline
→ Configure source connector (CSV / SQL / API)
→ Sink: sales_lakehouse / Tables / bronze_*
```

**4. Transformation (Silver)**
```
Workspace → New → Notebook
→ Load bronze tables via Spark
→ Apply cleansing logic
→ Write to silver_* Delta tables
```

**5. Semantic Model (Gold)**
```
Lakehouse → New Semantic Model
→ Select silver tables
→ Define relationships (star schema)
→ Add DAX measures
```

**6. Power BI Report**
```
Semantic Model → New Report
→ Build visuals and KPI cards
→ Publish to Workspace
```

---

## 🔮 Future Enhancements

- [ ] **Predictive analytics** — ML models for sales forecasting (Azure ML / Fabric ML)
- [ ] **Real-time streaming** — Eventstream integration for live transaction feeds
- [ ] **Automated anomaly detection** — Alert stakeholders on unusual sales patterns
- [ ] **Advanced customer segmentation** — RFM analysis and cohort modeling
- [ ] **Row-level security (RLS)** — Region/role-based data access in Power BI
- [ ] **CI/CD for pipelines** — Git integration and deployment pipelines in Fabric

---

## 👤 Author

**Jatin Vadile**


---

> *From raw data to boardroom insights — fully automated, fully unified.*
