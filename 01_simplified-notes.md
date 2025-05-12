# OLAP vs OLTP: Quick Reference Guide

## At a Glance

| OLTP | OLAP |
|:-----|:-----|
| **O**nline **T**ransaction **P**rocessing | **O**nline **A**nalytical **P**rocessing |
| Runs the business | Understands the business |
| Current operational data | Historical analytical data |
| Processes transactions | Processes insights |

## Key Differences

💼 **Purpose**
- **OLTP**: Day-to-day operations (orders, payments)
- **OLAP**: Business analysis and decision support

🔄 **Operations**
- **OLTP**: Many small, simple transactions (INSERT, UPDATE, DELETE)
- **OLAP**: Few complex queries with aggregations (SELECT with GROUP BY)

⏱️ **Performance**
- **OLTP**: Millisecond response time
- **OLAP**: Seconds to minutes response time

📊 **Data Model**
- **OLTP**: Normalized (3NF+) to minimize redundancy
- **OLAP**: Denormalized dimensional models (Star/Snowflake)

📋 **Schema Quick Look**

OLTP: Entity-Relationship Model
```
Customer → Orders → Order_Items → Products
        ↘ Payments
```

OLAP: Star Schema
```
           ┌─ Date Dimension
           │
Sales Fact ─┼─ Product Dimension
           │
           └─ Customer Dimension
```

## OLTP Flashcards

**Definition**: System that manages day-to-day transaction processing

**Optimized for**: Write performance (INSERT, UPDATE, DELETE)

**Example**: Processing a customer order on an e-commerce site

**Users**: Clerks, customers, applications (thousands)

**Data size**: Gigabytes (current operational data)

**Schema type**: Highly normalized (3NF+)

**Example systems**: MySQL, PostgreSQL, Oracle, SQL Server

## OLAP Flashcards

**Definition**: System that supports complex data analysis

**Optimized for**: Read performance (complex SELECT queries)

**Example**: Analyzing quarterly sales trends by region

**Users**: Analysts, executives, data scientists (hundreds)

**Data size**: Terabytes/Petabytes (historical data)

**Schema types**: 
- Star schema (fact table + dimension tables)
- Snowflake schema (normalized dimensions)

**Example systems**: Snowflake, Redshift, BigQuery, Analysis Services

## Quick Query Comparison

**OLTP Query**: Find a specific customer's recent orders
```sql
SELECT order_id, date, total 
FROM orders 
WHERE customer_id = 1234 
ORDER BY date DESC LIMIT 10;
```

**OLAP Query**: Analyze regional sales by product category
```sql
SELECT region, category, SUM(sales) as total_sales
FROM sales_fact
JOIN date_dim ON sales_fact.date_key = date_dim.date_key
JOIN product_dim ON sales_fact.product_key = product_dim.product_key
JOIN geography_dim ON sales_fact.geo_key = geography_dim.geo_key
WHERE date_dim.year = 2023
GROUP BY region, category
ORDER BY total_sales DESC;
```

## Data Flow Simplified

```
OLTP Systems → ETL/ELT → Data Warehouse (OLAP) → BI Tools
(Capture)       (Move)     (Analyze)              (Visualize)
```