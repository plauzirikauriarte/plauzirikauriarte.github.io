---
layout: default
title: Sales Analysis Dashboard | Power BI + SQL
permalink: /projects/sales-analysis-powerbi/
project-date: 2024
project-category: Business Intelligence
---

<div class="project-header">
  <a href="/projects/" class="back-link">← Back to Projects</a>
  <h1>Sales Analysis Dashboard</h1>
  <p class="project-subtitle">Interactive Power BI dashboard for sales analytics using SQL and AdventureWorks dataset</p>
</div>

---

## Project Overview

A comprehensive business intelligence dashboard designed to provide real-time insights into sales performance, regional trends, and product analytics. This project demonstrates end-to-end BI implementation from data extraction to interactive visualization.

**Key Focus:** Creating actionable insights through interactive dashboards and strategic metrics.

---


## Data Model

### Data Sources
- **Primary Dataset:** AdventureWorks OLTP Database
- **Tables Used:**
  - `Sales.SalesOrderHeader` - Order transactions
  - `Sales.SalesOrderDetail` - Order line items
  - `Sales.Customer` - Customer information
  - `Sales.SalesTerritory` - Regional data
  - `Production.Product` - Product details
  - `Production.ProductCategory` - Product hierarchy

### Data Model Structure

<img src="/projects/salesanalysisassets/star-schema.png"
     alt="Star Schema Data Model"
     width="900">


---

## Sample Screenshots

### Sales Overview

<img src="/projects/salesanalysisassets/aw - sales 1.png"
     alt="Adventure Works Sales Dashboard"
     width="900">

This page provides an overview of sales, costs, margin and order volume, allowing users to analyze performance by country, quarter and product family.

---

### Sales Overview - year 2013 selected to get YoY comparisons

<img src="/projects/salesanalysisassets/aw - sales 2.png"
     alt="Adventure Works Product Analysis"
     width="900">

---


## Salmple DAX Formulas

### Measure: Sales YoY Growth

```dax
SalesYoY = VAR CurrentYear = YEAR(TODAY())
RETURN
    CALCULATE(
        [TotalSales],
        YEAR(FactSales[OrderDate]) = CurrentYear
    )
```

### Measure: Total Sales

```dax
Sales Amount YoY % = 
IF(
    HASONEVALUE(DimDates[CalendarYear]),
    DIVIDE([Ventas totales] - [Sales Amount LY], [Sales Amount LY]),
    BLANK()
)
```

---

## Business Insights

- United States generated approximately one-third of total sales and remained the company's strongest market.
- Australia represented the second largest contributor, consolidating more than 25% of revenue.
- Road Bikes accounted for over 50% of total sales volume.
- Touring products experienced significant growth during the final periods analysed.
- Sales showed a positive trend throughout the year, reaching the highest level in the last quarter.

---

## Repository & Links

📁 **GitHub Repository:** [[Link to Repository](https://github.com/plauzirikauriarte)]


---

## Related Projects

---

<div class="project-navigation">
  <a href="/projects/" class="back-link">← Back to All Projects</a>
  <a href="/contact/" class="contact-link">Have questions? Contact me →</a>
</div>

<style>
.project-header {
  margin-bottom: 3rem;
}

.back-link {
  display: inline-block;
  margin-bottom: 1.5rem;
  color: #00d4ff;
  text-decoration: none;
  font-weight: 600;
  transition: color 0.3s ease;
}

.back-link:hover {
  color: #0099cc;
}

.project-header h1 {
  margin-bottom: 0.5rem;
}

.project-subtitle {
  font-size: 1.2rem;
  color: #666;
  font-weight: 500;
}

code {
  background: #f5f5f5;
  padding: 0.2rem 0.5rem;
  border-radius: 4px;
  font-family: 'Monaco', 'Menlo', monospace;
  font-size: 0.9rem;
}

pre {
  background: #1e3a5f;
  color: #00d4ff;
  padding: 1.5rem;
  border-radius: 8px;
  overflow-x: auto;
  font-size: 0.85rem;
  line-height: 1.5;
}

pre code {
  background: none;
  color: inherit;
  padding: 0;
}

.project-navigation {
  display: flex;
  justify-content: space-between;
  gap: 1rem;
  margin-top: 3rem;
  padding-top: 2rem;
  border-top: 2px solid #e0e0e0;
}

.contact-link {
  display: inline-block;
  color: #00d4ff;
  text-decoration: none;
  font-weight: 600;
  transition: color 0.3s ease;
}

.contact-link:hover {
  color: #0099cc;
}

@media (max-width: 768px) {
  .project-navigation {
    flex-direction: column;
  }
}
</style>
