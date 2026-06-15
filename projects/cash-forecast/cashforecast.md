---
layout: default
title: Corporate Cash Forecast & Ageing Dashboard | Excel BI
permalink: /projects/cash-forecast/
project-date: 2026
project-category: Financial Analytics & Business Intelligence
---

<div class="project-header">
  <a href="/projects/" class="back-link">← Back to Projects</a>
  <h1>Corporate Cash Forecast & Ageing Dashboard</h1>
  <p class="project-subtitle">Advanced liquidity forecasting and accounts receivable/payable analysis using Excel's BI Stack (Power Query + Power Pivot + DAX)</p>
</div>

---

## Project Overview

A robust, corporate-grade cash forecasting system designed to bridge the gap between raw ERP extracts and strategic financial decisions. This project solves a critical financial pain point: transforming fragmented data of bank balances, pending invoices, and future horizons into a dynamic, reliable liquidity runway.

**Key Focus:** Ensuring data integrity through financial logic, automated ETL pipelines, and user-centric dashboard design.

---

## Data Model & Architecture

### Data Sources
- **ERP Exports (Excel/CSV):** Extract files detailing pending accounts receivable (Cobros) and accounts payable (Pagos).
- **Bank Ledger Data:** Historical and current bank account balances for initial cash status.
- **Auxiliary Mapping Tables:** Custom dimension tables created to standardize client/supplier grouping and calendar horizons.

### Architecture & Next Steps
The project implements a classic BI architectural workflow: **Extract ➔ Transform ➔ Model ➔ Visualize**. 

> 💡 **Future Automation Roadmap:** As a scalable next step, the manual Excel/CSV extractions from the ERP will be replaced by a direct pipeline via SQL database connections or API integrations, eliminating manual file downloads completely.

---

## Sample Screenshots

### Liquidity Forecast & Financial Core

<img src="/projects/cashforecastassets/dashboard-main.png" 
     alt="Cash Forecast Main Dashboard" 
     width="900">

The central core links dynamic bank tracking with interactive timeline slices. It features integrated conditional formatting utilizing corporate-aligned color palettes (`HEX` matched to the company brand) and fully custom UI/UX elements. 

---

### Interactive Filtering & Ageing Analysis

<img src="/projects/cashforecastassets/dashboard-filtered.png" 
     alt="Filtered Client Analysis" 
     width="900">

The dashboard includes tailored slicers connected directly to the core data model. When an individual client or supplier is selected, the system isolating their upcoming maturities instantly.

---

## Sample DAX Formulas & Financial Logic

### Prevent Non-All Slicer Distortion (Data Integrity)
To prevent management from making decisions based on unrealistic bank data when filtering specific clients, a custom logic block was built into the starting and ending balance cells:

```excel
=SI(O(Análisis!$AF$1<>"All";Análisis!$AJ$1<>"All");"";Análisis!H3)
