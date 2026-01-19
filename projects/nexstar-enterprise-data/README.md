# Enterprise Data Architecture – NexStar Finance

## The Problem
NexStar Finance is a global fintech operating across the United States, Latin America, and Africa. Its customer, transaction, and vendor data existed in siloed systems, preventing leadership from accessing real-time insights, increasing fraud risk, and creating compliance exposure.

## What I Built
I designed a cloud-native enterprise data platform that unified all customer, transaction, and vendor data into a single governed analytics environment.

## Tools Used
SQL · Data Modeling · Cloud Data Warehousing · DAMA-DMBOK · TOGAF · Data Governance

## What I Did
- Designed a three-table relational schema (Customers, Transactions, Vendors)
- Built 10 SQL queries for executive reporting, fraud detection, and compliance
- Designed a Snowflake-style cloud data warehouse architecture
- Created an 18-month enterprise data modernization roadmap
- Implemented data governance, metadata, and data-quality frameworks

## Business Impact
This solution enables:
- Real-time enterprise reporting  
- Unified customer and transaction views  
- Regulatory compliance (GDPR, CCPA)  
- Scalable analytics for global expansion  

This project demonstrates enterprise-scale data architecture, analytics engineering, and governance design for a real-world fintech environment.
## Data Model
Customers Table
CREATE TABLE Customers (
    customer_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    region VARCHAR(50),
    account_created DATE
);

Vendors Table
CREATE TABLE Vendors (
    vendor_id INT PRIMARY KEY,
    vendor_name VARCHAR(100),
    service_type VARCHAR(50),
    region VARCHAR(50),
    compliance_rating VARCHAR(20)
);

Transactions Table
CREATE TABLE Transactions (
    transaction_id INT PRIMARY KEY,
    customer_id INT,
    vendor_id INT,
    amount DECIMAL(10,2),
    transaction_date DATE,
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id),
    FOREIGN KEY (vendor_id) REFERENCES Vendors(vendor_id)
);



## SQL Analytics
# Sample Analytical SQL Queries

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


