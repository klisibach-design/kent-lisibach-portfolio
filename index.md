# Kent Lisibach  
### Data Analyst | Data Warehouse | Decision Analytics  

I design data systems that turn fragmented, messy data into reliable insights for business, compliance, and decision-making.

**Specialties:**  
SQL · Power BI · Data Modeling · Cloud Data Warehousing · R · Enterprise Data Architecture  

---

## Projects

| Project | Description |
|--------|-------------|
| [Enterprise Data Architecture – NexStar Finance](projects/nexstar-enterprise-data.md) | Built a cloud data warehouse, SQL analytics, and governance model for a global fintech |
| [Higher-Education ROI Decision Model](projects/higher-ed-roi.md) | Power BI decision tree analyzing which college majors generate the highest financial return |
| [Climate Data Analysis in R](projects/climate-data.md) | Statistical comparison of USA vs UK climate patterns |

---
📄 **Resume coming soon**

## Sample Analytical SQL Queries

The following queries demonstrate common analytical operations used to support reporting, compliance monitoring, and financial insights.
Query 1: Total number of customers

SELECT COUNT(*) AS total_customers
FROM Customers;



Query 2: Count Customers by Region

SELECT region, COUNT(*) AS customers_per_region
FROM Customers
GROUP BY region;

Query 3: Minimum Transaction Amount

SELECT MIN(amount) AS minimum_transaction
FROM Transactions;

Query 4: Maximum Transaction Amount

SELECT MAX(amount) AS maximum_transaction
FROM Transactions;

Query 5: Transactions Over $500

SELECT *
FROM Transactions
WHERE amount > 500;

Query 6: Transactions Ordered by Amount

SELECT *
FROM Transactions
ORDER BY amount DESC;

Query 7: Join Customers and Transactions

SELECT
    c.first_name,
    c.last_name,
    t.transaction_id,
    t.amount,
    t.transaction_date
FROM Customers c
JOIN Transactions t
    ON c.customer_id = t.customer_id;

Query 8: Total Transaction Amount Per Customer

SELECT
    c.first_name,
    c.last_name,
    SUM(t.amount) AS total_spent
FROM Customers c
JOIN Transactions t
    ON c.customer_id = t.customer_id
GROUP BY c.first_name, c.last_name;

Query 9: Count Transactions Per Vendor

SELECT
    v.vendor_name,
    COUNT(t.transaction_id) AS transaction_count
FROM Vendors v
JOIN Transactions t
    ON v.vendor_id = t.vendor_id
GROUP BY v.vendor_name;

Query 10: High-Value Transactions With Customer Names

SELECT
    c.first_name,
    c.last_name,
    v.vendor_name,
    t.amount,
    t.transaction_date
FROM Transactions t
JOIN Customers c
    ON t.customer_id = c.customer_id
JOIN Vendors v
    ON t.vendor_id = v.vendor_id
WHERE t.amount > 500;
