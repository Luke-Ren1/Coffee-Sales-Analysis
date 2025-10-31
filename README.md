# Coffee Sales Analysis

## Project Overview
Brief description of your coffee sales analytics project.

## Dataset Description
Information about the dataset used in this analysis.

## Database Setup

### Creating Tables in PostgreSQL

Here, we need to first create the table where our data will live in.
```sql
CREATE TABLE coffee_sales
(hour_of_day numeric,
cash_type text,
money numeric,
coffee_name text,
time_of_day text,
weekday text,
month_name text,
weekdaysort numeric,
monthsort numeric,
date date
);
```
The column names need to match the data source, and the data type must match!

### Importing CSV Data
Find the location of our data, and use this code to input our data into the table we created earlier
```sql
COPY coffee_sales
FROM 'D:\Data Analysis\Data Sets\Coffe_sales.csv'
DELIMITER ','
CSV HEADER;
```

## SQL Business Analysis
### ☕ Product Performance
**1. Which is the top-selling coffee?**
```sql
Select 
	coffee_name,
	count(*) AS times_ordered,
	ROUND(SUM(money),2) AS total_revenue
FROM
	coffee_sales
GROUP BY
	coffee_name
ORDER BY
	total_revenue desc
```
**Answer:**

<img width="477" height="297" alt="image" src="https://github.com/user-attachments/assets/3755de14-1ef6-42ee-b98e-dd2ff431a370" />
- In terms of revenue, Latte is the best-selling coffee
  
- In terms of order, Americano with milk is the best-selling coffee

***

**2. What is the price range for each coffee type?**
```sql
SELECT 
    coffee_name,
    ROUND(MAX(money),2) AS max_price,
    ROUND(MIN(money),2) AS min_price,
    ROUND(AVG(money),2) AS avg_price
FROM coffee_sales
GROUP BY coffee_name
ORDER BY avg_price DESC;
```
**Answer:**

<img width="531" height="291" alt="image" src="https://github.com/user-attachments/assets/bf777a4d-8e05-48c9-bc2e-86de7cff2580" />


### 🕒 Time-Based Analysis
**3. Which time of day brings in the most revenue?**
```sql
SELECT
	time_of_day,
	SUM(money) AS total_revenue
FROM
	coffee_sales 
GROUP BY
	time_of_day
ORDER BY
	total_revenue desc
```
**Answer:**
<img width="300" height="143" alt="image" src="https://github.com/user-attachments/assets/4cbd5a52-0ada-4d0a-b0df-751aaff11081" />


### Sales Performance Analysis
SQL queries analyzing sales trends, revenue, and performance metrics.

### Product Analysis
Analysis of product performance, top-selling items, and category performance.

### Customer Analysis
Insights into customer behavior, segmentation, and purchasing patterns.

### Seasonal Trends Analysis
Queries examining seasonal patterns and time-based trends.

## Key Findings
Summary of the most important insights discovered through the analysis.

## Business Recommendations
Actionable recommendations based on the SQL analysis results.

## Tools Used
- PostgreSQL
- SQL
- (Add any other tools you used)

## How to Run This Analysis
Instructions for reproducing the analysis.

## Files in This Repository
- [Raw Dataset](powerbi/dax_calculations.md)
- `sql_queries.sql`: All SQL queries used in the analysis
- `analysis_results.md`: Summary of findings
