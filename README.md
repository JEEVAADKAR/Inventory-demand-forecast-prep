# Inventory Demand Forecast Preparation

## Overview
This project focuses on preparing historical sales and inventory data for demand forecasting.
The workflow includes extracting data from a MySQL database, cleaning and transforming it using Excel Power Query, and organizing it into a structured, forecast-ready format.

The final output can be directly used for inventory demand forecasting in Excel, Python, or BI tools.

---

## Objectives
- Extract historical sales and stock level data from MySQL
- Clean and merge datasets by product and month
- Handle missing sales values and small data gaps
- Create a pivoted, time-series dataset ready for forecasting

---

## Tools & Technologies
- **MySQL Workbench**
- **SQL**
- **Microsoft Excel**
- **Excel Power Query**

---

## Data Description
### Tables Used
- **Salestask Table**
  - `product_id`
  - `sale_date`
  - `quantity_sold`

- **Inventorytask Table**
  - `product_id`
  - `stock_date`
  - `stock_level`

---

## SQL Data Extraction
Sales and inventory data were aggregated at a monthly level using SQL queries.

### Monthly Sales Query
```sql
SELECT 
    product_id,
    DATE_FORMAT(sale_date, '%Y-%m') AS sale_month,
    SUM(quantity_sold) AS total_sold
FROM sales
GROUP BY product_id, sale_month;
SELECT 
    product_id,
    DATE_FORMAT(stock_date, '%Y-%m') AS stock_month,
    MAX(stock_level) AS stock_level
FROM inventory
GROUP BY product_id, stock_month;

Data Cleaning & Transformation (Excel Power Query)

Loaded CSV files into Excel using Power Query
Converted date columns to consistent month formats
Merged sales and inventory data using product_id and month
Replaced missing sales values with zero or interpolated small gaps
Forward-filled missing stock values
Sorted data chronologically
Pivoted data by product and month

Final Output:

The final dataset is structured as a product-wise monthly sales matrix:

Product ID	Jan	Feb	Mar
101	20	15	20
102	5	15	10
103	20	18	25

This format is suitable for:

Demand forecasting
Trend analysis
Inventory planning
