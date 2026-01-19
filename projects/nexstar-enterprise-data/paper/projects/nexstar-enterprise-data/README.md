# Enterprise Data Architecture & SQL Analysis – NexStar Finance

## Overview
This project demonstrates enterprise data modeling and SQL analysis for a fictional global fintech company, **NexStar Finance**. The goal was to design a normalized relational schema and use SQL to generate business-relevant insights related to customers, transactions, and vendors.

The project emphasizes:
- Relational database design
- SQL aggregation, filtering, and joins
- Translating business questions into queries
- Enterprise data governance concepts

📄 **Full written report (PDF):**  
[nexstar_enterprise_data_management.pdf](./nexstar_enterprise_data_management.pdf)

---

## Data Model

A three-table relational schema was designed to support centralized analytics and reporting.

### Tables Created

**Customers**
- `customer_id` (PK)
- `first_name`
- `last_name`
- `region`
- `account_created`

**Transactions**
- `transaction_id` (PK)
- `customer_id` (FK)
- `vendor_id` (FK)
- `amount`
- `transaction_date`

**Vendors**
- `vendor_id` (PK)
- `vendor_name`
- `service_type`
- `region`
- `compliance_rating`

### Schema Diagram

![Relational Schema](./Relational%20data%20model.jpg)


---

## SQL Queries

Ten SQL queries were written to demonstrate core analytical patterns used in enterprise reporting.

### Query Summary

| # | Query Purpose | SQL Concepts |
|---|--------------|-------------|
| 1 | Count total customers | `COUNT()` |
| 2 | Customers by region | `COUNT()`, `GROUP BY` |
| 3 | Minimum transaction amount | `MIN()` |
| 4 | Maximum transaction amount | `MAX()` |
| 5 | High-value transactions | `WHERE` |
| 6 | Sort transactions by amount | `ORDER BY` |
| 7 | Customer transaction history | `JOIN` |
| 8 | Total spend per customer | `JOIN`, `SUM()` |
| 9 | Transactions per vendor | `JOIN`, `COUNT()` |
|10 | High-value transactions with names | `JOIN`, `WHERE` |

---

## Example SQL Queries


```sql

### Customers by Region
SELECT region, COUNT(*) AS customer_count
FROM customers
GROUP BY region;

### High-Value Transactions with Customer & Vendor Names
SELECT c.first_name,
       c.last_name,
       v.vendor_name,
       t.amount
FROM transactions t
JOIN customers c
  ON t.customer_id = c.customer_id
JOIN vendors v
  ON t.vendor_id = v.vendor_id
WHERE t.amount > 500;


