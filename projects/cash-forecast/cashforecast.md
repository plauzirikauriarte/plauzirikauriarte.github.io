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

> 🔒 **Confidentiality Notice:** This dashboard is built upon a **real-world corporate project**. To comply with data privacy and NDA standards, all sensitive company names, client/supplier details, financial balances, and transaction values have been fully anonymized and synthetically scaled. The original relational logic and analytical structure remain completely intact.

---

## Data Model & Architecture

### Data Sources
- **ERP Exports (Excel/CSV):** Extract files detailing pending accounts receivable (Cobros) and accounts payable (Pagos).
- **Bank Ledger Data:** Historical and current bank account balances for initial cash status.
- **Auxiliary Mapping Tables:** Custom dimension tables created to standardize client/supplier grouping and calendar horizons.

### Architecture & Next Steps
The project implements a classic BI architectural workflow: **Extract ➔ Transform ➔ Model ➔ Visualize**. 

> 💡 **Future Automation Roadmap:** As a scalable next step, the manual Excel/CSV extractions from the ERP will be replaced by a direct pipeline via SQL database connections or API integrations, eliminating manual file downloads completely.

### Data Model Structure

<img src="/projects/cash-forecast/Cash forecast PLU - data model edit.png" 
     alt="Filtered Client Analysis" 
     width="900">

The relational data model implemented in Power Pivot, structured around a tailored Star Schema. At its core, a dynamic 30-day forecast table acts as the primary calendar dimension, bridging the gap between current bank ledger data, auxiliary data tables, and future cash flow projections (Accounts Receivable and Accounts Payable fact tables). A dedicated measures table centralizes all financial DAX logic.

---

## Sample Screenshots

### Liquidity Forecast & Financial Core

<img src="/projects/cash-forecast/Cash forecast PLU - 1.png" 
     alt="Cash Forecast Main Dashboard" 
     width="900">

The central core links dynamic bank tracking with interactive timeline slices. It features integrated conditional formatting utilizing corporate-aligned color palettes (`HEX` matched to the company brand) and fully custom UI/UX elements. 

---

### Interactive Filtering & Ageing Analysis

<img src="/projects/cash-forecast/Cash forecast PLU - 2.png" 
     alt="Filtered Client Analysis" 
     width="900">

The dashboard includes tailored slicers and option buttons connected directly to the core data model. The option button allows the user to analyze the cash flows including or excluding group companies (in this case, "Cliente 27" and "Proveedor 78"). Regarding the week slicer, when a week is selected, the Top 10 Customers and Suppliers chart bellow change according to that selection.

---
### Overdue / Next 30 days / Future 

<img src="/projects/cash-forecast/Cash forecast PLU - 3.png" 
     alt="Filtered Client Analysis" 
     width="900">

---

### Customer and Supplier filtering

<img src="/projects/cash-forecast/Cash forecast PLU - 4.png" 
     alt="Filtered Client Analysis" 
     width="900">

This filters inmediately make changes in the main table on the left by just showing the expected payments or collections in the following 30 days. When this charts are filtered, the forecast table on the left stops showing both the expected initial and final balance for each day and the up/down arrow mark.

---

## Sample DAX Formulas & Advanced Calculations

The project centralizes its financial logic inside a unified Measures repository. Below are the 5 most advanced DAX calculations developed to handle cash accumulation, dynamic ledger balancing, and temporal horizons.

### 1. Dynamic Daily Cash Position (Ending Balance)
This measure calculates the actual cash available at the end of any given day. It takes the initial bank balance and adds the cumulative net flow (collections minus payments) up to that specific point in time.

```dax
Saldo final = 
VAR MaxFecha = MAX('Calendario prox 30 días'[Date])
RETURN
    [Saldo inicial prev] + 
    CALCULATE(
        [Flujo Neto],
        FILTER(
            ALL('Calendario prox 30 días'),
            'Calendario prox 30 días'[Date] <= MaxFecha
        )
    )
```

### 2. Rolling Cumulative Net Cash Flow
To plot the liquidity runway graph without time-gap distortions, this measure calculates the running total of the net cash flow. It explicitly evaluates the data state across the custom calendar dimension.

```dax
Flujo Neto Acum = 
VAR MaxFecha = MAX('Calendario prox 30 días'[Date])
RETURN
    CALCULATE(
        [Flujo Neto],
        FILTER(
            ALLSELECTED('Calendario prox 30 días'),
            'Calendario prox 30 días'[Date] <= MaxFecha
        )
    )
```

### 3. Smart Extraction of Current Bank Ledger
This measure extracts the baseline cash status from the bank statement table. It isolates the last known balance entry before the forecasting timeline begins, ensuring the projection starts from a verified mathematical real-world figure.

```dax
Saldo inicial prev = 
CALCULATE(
    SUM('PLU - saldos bancarios'[Saldo]),
    LASTDATE('PLU - saldos bancarios'[Fecha])
)
```

### 4. Dynamic Time Horizon Classification (Ageing Categorization)
This calculated column logic shifts transactions dynamically into operational windows (Overdue, Next 7 Days, Horizon). It enables the dashboard's semantic semaphores to switch states automatically based on the current date execution.

```dax
atrasados/próximos/posteriores = 
VAR FechaVenc = 'PLU - cobros pendientes'[Fecha Vencimiento]
VAR Hoy = TODAY()
RETURN
    SWITCH(
        TRUE(),
        FechaVenc < Hoy, "Atrasado",
        FechaVenc >= Hoy && FechaVenc <= Hoy + 7, "Próximos 7 días",
        "Posterior"
    )
```

### 5. Consolidated Net Cash Flow (The Core Ledger Link)
The atomic engine of the forecasting model. It aggregates uncollected revenues (Cobros) and subtracts pending expenses (Pagos) and corporate payrolls (Nóminas) across a unified relational matrix, driving every single visual layout in the system.

```dax
Flujo Neto = [Total cobros pendientes] - [Total pagos pendientes] - SUM('Nóminas y SS'[IMPORTE])
```

---
