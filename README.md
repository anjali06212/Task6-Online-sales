Online Sales Trend Analysis
By: Anjali DS

Description
This project performs a sales trend analysis by aggregating monthly revenue and order volume from e-commerce data using PostgreSQL.
The analysis uses SQL to group data by month and year, calculate total revenue, and measure order volume, enabling clear visualization of sales trends.
It is compatible with PostgreSQL, MySQL, and SQLite.

Features
SQL Query:

Uses EXTRACT (or dialect equivalents) for month/year.

Calculates Total Revenue using SUM(amount).

Calculates Order Volume using COUNT(DISTINCT product_id).

Sorts results chronologically.

Sample Data:

Input CSV (online_sales_dataset_sample.csv) with 48 sample records (2 per month for 24 months).

Includes product_id, order_date, and amount.

Results:

Output CSV (sales_trend_analysis_results.csv) with aggregated data for January 2023 to December 2024.

Repository Structure
sales_trend_analysis.sql – SQL script to:

Create the orders table.

Insert sample data.

Run the aggregation query.

online_sales_dataset_sample.csv – Sample e-commerce input data.

sales_trend_analysis_results.csv – Aggregated results (24 months of data).

Prerequisites
A database system:

PostgreSQL (recommended)

MySQL or SQLite (with slight syntax modifications)

A tool to execute SQL queries:

pgAdmin, MySQL Workbench, or SQLite CLI

Setup & Usage
1️ Set Up the Database
Option A — Run the CREATE TABLE and INSERT statements from sales_trend_analysis.sql:

sql
Copy
Edit
CREATE TABLE orders (
    product_id VARCHAR(50),
    order_date DATE,
    amount DECIMAL(10, 2)
);
Option B — Create the table and import online_sales_dataset_sample.csv using:

PostgreSQL → COPY command

MySQL → LOAD DATA INFILE

SQLite → .import

2️ Run the Analysis Query
PostgreSQL version:

sql
Copy
Edit
SELECT 
    EXTRACT(YEAR FROM order_date) AS year,
    EXTRACT(MONTH FROM order_date) AS month,
    TO_CHAR(order_date, 'Month') AS month_name,
    SUM(amount) AS total_revenue,
    COUNT(DISTINCT product_id) AS order_volume
FROM orders
GROUP BY year, month, month_name
ORDER BY year, month;
3️ Adaptations for Other Databases
MySQL:

YEAR(order_date)

MONTH(order_date)

MONTHNAME(order_date)

SQLite:

strftime('%Y', order_date)

strftime('%m', order_date)

strftime('%B', order_date)

Results Summary
Example from sales_trend_analysis_results.csv (first 5 rows):

year	month	month_name	total_revenue	order_volume
2023	1	January	150,250.50	325
2023	2	February	132,450.75	280
2023	3	March	165,780.20	350
2023	4	April	140,320.10	300
2023	5	May	145,670.80	310
    
#Notes
The sample dataset is simplified. Real-world analysis should use larger datasets.

You can filter by year or quarter using a WHERE clause.

Extend the query to include additional metrics like average order value or growth rate.

