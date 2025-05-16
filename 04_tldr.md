# OLAP vs OLTP: TLDR

## OLTP (Online Transaction Processing)

* **OLTP** stands for **Online Transaction Processing**
* Used for recording transactional records from customer-facing applications
* Data model is highly normalized with each object as its own entity
* Data linked via relationships (Primary Keys, Foreign Keys)
* Optimized for writing operations, with slightly slower reading
* Requires multiple joins to display comprehensive data in a single view
* Easily joins 2-3 tables together via PK/FK relationships
* Prioritizes data capture, integrity, and storage
* Implements traditional relational database design (Entity-Relationship Diagrams)
* Examples: PostgreSQL, MySQL, Oracle, SQL Server, MongoDB (NoSQL)
* Ensures no data redundancy, loss, or inconsistency
* Response time typically in milliseconds

## OLAP (Online Analytical Processing)

* **OLAP** stands for **Online Analytical Processing**
* Used for business analytics to drive decision-making
* Helps understand user behavior and business performance
* Extracts insights to improve business strategy, products, and marketing
* Prioritizes reading performance over writing
* Data model is partially denormalized
* Follows star schema (fact table + dimension tables) or snowflake schema
* Designed for complex queries across multiple tables
* Built for business analysis with easy data aggregation
* Storage options include data lakes, data warehouses, and data lakehouses
  * Data lakes: AWS S3, Azure Data Lake, Google Cloud Storage
  * Data warehouses: AWS Redshift, Azure Synapse, Google BigQuery
  * Data lakehouses: AWS SageMaker Lakehouse, Databricks
* Requires ETL/ELT pipelines (often using PySpark)
* Response time typically in seconds to minutes
* Handles terabytes to petabytes of data

## OLTP vs OLAP: The Relationship

* OLTP is the first step: capture user/customer data quickly and reliably
* OLAP uses data stored from OLTP for analytics and decision-making
* **OLTP records the business** while **OLAP understands the business**
* OLTP focuses on current operational data; OLAP leverages historical data
* OLTP handles many small, simple transactions; OLAP processes few complex queries
* OLTP serves thousands of users (clerks, customers); OLAP serves hundreds (analysts, executives)
* Data flows: OLTP Systems → ETL/ELT → Data Warehouse (OLAP) → BI Tools
* Both paradigms are essential for a complete data strategy:
  * Record business operations via OLTP
  * Upgrade business strategy via OLAP