# Palladium Bank: Retail Banking Dimensional Data Warehouse Design

## Project Overview

This project focuses on designing a dimensional data warehouse solution for Palladium Bank to improve reporting performance, analytical consistency, and scalability.

The bank currently relies on raw transaction logs for reporting, resulting in slow queries and inconsistent business metrics. A star schema dimensional model was designed to support customer behavior analysis, branch performance monitoring, product analysis, churn detection, and time-based reporting.

---

## Business Problem

The Retail Banking division required a scalable analytics platform capable of answering critical business questions:

- Which customer segments generate the highest fee income?
- How does transaction behavior vary by branch and channel?
- Are high-value customers reducing activity?
- Which banking products drive deposits and withdrawals?
- How can reporting performance be improved across the organization?

---

## Data Modeling Approach

A dimensional modeling approach was selected to separate descriptive business attributes from measurable transactional data.

### Fact Table Grain

The fact table was designed at the transaction level:

> One row represents one banking transaction.

This grain supports detailed transaction analysis while maintaining flexibility for aggregation.

---

## Data Profiling & Dimension Identification

### Dimensions

- Customer Dimension
- Branch Dimension
- Product Dimension
- Channel Dimension
- Date Dimension

### Fact Table

- Fact Transactions

### Degenerate Dimension

- Transaction ID

Surrogate keys were introduced across all dimensions to improve performance and support Slowly Changing Dimensions (SCD).

---

## Star Schema Design

The solution follows a star schema architecture consisting of:

### Fact Table

- fact_transactions

### Dimension Tables

- dim_customer
- dim_branch
- dim_product
- dim_channel
- dim_date

### Aggregation Table

- agg_monthly_branch_performance

The aggregation table stores monthly transaction totals by branch to improve reporting performance.

---

## Slowly Changing Dimensions (SCD)

### SCD Type 2

Implemented for:

- Customer Dimension
- Product Dimension

This preserves historical changes while maintaining accurate historical reporting.

### SCD Type 1

Implemented for:

- Branch Dimension

Current values overwrite previous values where historical tracking is not required.

---

## ETL / ELT Strategy

An ELT (Extract, Load, Transform) approach was selected.

### Initial Load Process

1. Extract raw transaction data
2. Load data into staging tables
3. Populate dimensions
4. Generate surrogate keys
5. Validate data quality
6. Populate fact table

### Incremental Load Strategy

- Detect new transactions using Transaction ID and Transaction Date
- Apply SCD Type 1 and Type 2 updates
- Prevent duplicate fact records
- Maintain referential integrity

---

## Data Quality Framework

The model incorporates:

1. Null Validation
2. Duplicate Detection
3. Referential Integrity Checks
4. Data Type Validation

Failed records are flagged and reviewed before loading.

---

## Performance & Scalability

### Partitioning

Fact table partitioning by transaction date.

### Indexing

Indexes applied on:

- Surrogate Keys
- Foreign Keys
- Transaction Date

### Aggregation

Monthly branch-level aggregation table created to improve reporting speed.

---

## Reporting Hierarchies

### Time Hierarchy

Year → Quarter → Month

### Geography Hierarchy

State → Branch

These hierarchies support drill-down analysis in BI reporting tools.

---

## Tools & Technologies

- PostgreSQL
- SQL
- PowerPoint
- Dimensional Modeling
- Star Schema Design
- Data Warehousing Concepts

---

## Author

**Hassan Mistura**  
Data Analyst
