# Retail Sales SQL Project

## Project Overview
This project analyzes retail sales data using structured SQL queries. The objective is to extract valuable insights from the sales database, such as revenue trends, customer purchasing behavior, and product performance metrics. The queries facilitate effective data-driven decision-making.

## Files Included
- **sql_query_p1_retail_sales.sql**: A comprehensive set of SQL queries used for data analysis.

## Database Schema
The project uses a `retail_sales` table with the following structure:

```sql
CREATE DATABASE sql_project_p2;

DROP TABLE IF EXISTS retail_sales;

CREATE TABLE retail_sales (
    transaction_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(15),
    age INT,
    category VARCHAR(15),
    quantity INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);
```

## Data Cleaning
SQL queries used to clean the data:
```sql
SELECT * FROM retail_sales WHERE transaction_id IS NULL;
SELECT * FROM retail_sales WHERE sale_date IS NULL;
SELECT * FROM retail_sales WHERE sale_time IS NULL;

DELETE FROM retail_sales WHERE transaction_id IS NULL OR sale_date IS NULL OR sale_time IS NULL OR gender IS NULL OR category IS NULL OR quantity IS NULL OR cogs IS NULL OR total_sale IS NULL;
```

## Data Exploration
Some key queries:
```sql
-- Count total sales
SELECT COUNT(*) AS total_sale FROM retail_sales;

-- Count unique customers
SELECT COUNT(DISTINCT customer_id) AS unique_customers FROM retail_sales;

-- Distinct product categories
SELECT DISTINCT category FROM retail_sales;
```

## Data Analysis & Business Insights
Sample queries include:
```sql
-- Retrieve sales for a specific date
SELECT * FROM retail_sales WHERE sale_date = '2022-11-05';

-- Find transactions where the category is 'Clothing' and quantity > 4 in November 2022
SELECT * FROM retail_sales WHERE category = 'Clothing' AND TO_CHAR(sale_date, 'YYYY-MM') = '2022-11' AND quantity >= 4;

-- Calculate total sales for each category
SELECT category, SUM(total_sale) AS net_sale, COUNT(*) AS total_orders FROM retail_sales GROUP BY category;

-- Find average age of customers who purchased from 'Beauty' category
SELECT ROUND(AVG(age), 2) AS avg_age FROM retail_sales WHERE category = 'Beauty';

-- Find transactions where total_sale is greater than 1000
SELECT * FROM retail_sales WHERE total_sale > 1000;

-- Find total transactions by gender in each category
SELECT category, gender, COUNT(*) AS total_trans FROM retail_sales GROUP BY category, gender ORDER BY category;

-- Find best selling month in each year
SELECT year, month, avg_sale FROM (SELECT EXTRACT(YEAR FROM sale_date) AS year, EXTRACT(MONTH FROM sale_date) AS month, AVG(total_sale) AS avg_sale, RANK() OVER (PARTITION BY EXTRACT(YEAR FROM sale_date) ORDER BY AVG(total_sale) DESC) AS rank FROM retail_sales GROUP BY 1, 2) AS t1 WHERE rank = 1;

-- Find top 5 customers based on total sales
SELECT customer_id, SUM(total_sale) AS total_sales FROM retail_sales GROUP BY customer_id ORDER BY total_sales DESC LIMIT 5;

-- Find unique customers per category
SELECT category, COUNT(DISTINCT customer_id) AS cnt_unique_cs FROM retail_sales GROUP BY category;

-- Categorize sales into shifts (Morning, Afternoon, Evening)
WITH hourly_sale AS (
    SELECT *, CASE 
        WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
        WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'Evening' END AS shift
    FROM retail_sales
) 
SELECT shift, COUNT(*) AS total_orders FROM hourly_sale GROUP BY shift;
```

## Technologies Used
- **Database Management System (DBMS)**: MySQL / PostgreSQL / SQL Server (Specify the applicable DBMS)
- **SQL**: Structured Query Language for data extraction, manipulation, and analysis.

## Usage Instructions
1. Load the retail sales database into your preferred SQL environment.
2. Open the `sql_query_p1_retail_sales.sql` file using an SQL editor.
3. Execute individual queries to derive specific analytical insights.
4. Modify or optimize queries based on the dataset's unique structure and requirements.

## Expected Outcomes
Executing the provided SQL queries will yield:
- Breakdown of total revenue and category-wise sales
- Customer segmentation based on purchasing behavior
- Insights into product demand and best-selling items
- Monthly, quarterly, and annual sales trends

## Future Enhancements
- Implementation of stored procedures for automation
- Creation of SQL views for streamlined data access
- Integration with visualization tools (e.g., Tableau, Power BI) for enhanced reporting

## Author
Rudresh P
