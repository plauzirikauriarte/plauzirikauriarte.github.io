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

## Technologies Used

### BI & Visualization
- **Power BI Desktop** - Dashboard development
- **Power Query** - Data transformation
- **DAX (Data Analysis Expressions)** - Calculations and measures

### Data
- **AdventureWorks Sample Database** - OLTP dataset
- **Fact & Dimension Tables** - Star schema design
- **Date Dimension** - Time intelligence


---

## Dashboard Features

### 1. Executive Summary
- High-level KPIs (Total Sales, Orders, Customers)
- Year-to-Date metrics with targets
- Sales trend visualization
- Regional performance overview

### 2. Sales Analysis
- Sales by product category
- Sales by territory/region
- Sales by customer segment
- Top 10 products performance
- Sales trend over time

### 3. Regional Performance
- Sales by territory heatmap
- Regional comparison metrics
- Territory-level drill-down capability
- Regional growth trends

### 4. Product Analytics
- Product category performance
- Best-selling products
- Product profitability
- Product trend analysis
- Inventory insights

### 5. Interactive Filters
- Date range selector
- Territory/Region filter
- Product category filter
- Customer segment filter
- Year/Month/Quarter selection

---

## Screenshots

<img src="/projects/salesanalysisassets/sales-summary.png"
     alt="Sales Summary"
     width="900">

```
[Screenshot 1: Sales Summary]
KPIs displayed at the top with key metrics
```

---


## DAX Formulas

### Measure: Total Sales

```dax
TotalSales = SUMX(
    FactSales,
    FactSales[Quantity] * FactSales[UnitPrice]
)
```

### Measure: Sales YoY Growth

```dax
SalesYoY = VAR CurrentYear = YEAR(TODAY())
RETURN
    CALCULATE(
        [TotalSales],
        YEAR(FactSales[OrderDate]) = CurrentYear
    )
```

### Measure: Average Order Value

```dax
AvgOrderValue = DIVIDE(
    [TotalSales],
    DISTINCTCOUNT(FactSales[OrderID]),
    0
)
```

### Measure: Month-over-Month Growth

```dax
MoMGrowth = VAR CurrentMonth = [TotalSales]
    VAR PreviousMonth = CALCULATE(
        [TotalSales],
        DATEADD(DimDate[Date], -1, MONTH)
    )
RETURN
    DIVIDE(CurrentMonth - PreviousMonth, PreviousMonth, 0)
```

---

## Business Insights

### Key Findings

1. **Sales Concentration**
   - Top 20% of products generate 80% of revenue
   - Regional variations in product preferences
   - Seasonal patterns observed in Q4

2. **Customer Behavior**
   - Average customer lifetime value: [Value]
   - Repeat purchase rate: [%]
   - Customer acquisition cost: [Value]

3. **Growth Opportunities**
   - Emerging product categories showing growth
   - Underperforming regions with potential
   - Cross-selling opportunities identified

4. **Performance Metrics**
   - Quarter-over-quarter growth: [%]
   - Customer satisfaction metrics: [Value]
   - Order fulfillment rate: [%]


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
