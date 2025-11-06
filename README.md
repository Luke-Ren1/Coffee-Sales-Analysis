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

***

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


**4. What are the busiest hours of the day?**
```sql
SELECT
	hour_of_day,
	count(*) AS order_count
FROM
	coffee_sales
GROUP BY
	hour_of_day
ORDER BY
	order_count DESC
```
**Answer:** 

<img width="293" height="578" alt="image" src="https://github.com/user-attachments/assets/abd5500b-1266-4fb2-8eb4-84a3807d594a" />


**5. Which days of the week are busiest?**
```sql
SELECT
	weekday,
	count(*) AS order_count
FROM
	coffee_sales
GROUP BY
	weekday, weekdaysort
ORDER BY
	order_count DESC
```
**Answer:**

<img width="270" height="270" alt="image" src="https://github.com/user-attachments/assets/7704352d-c9c7-4395-9437-2f5dbca49cca" />


**6. How does weekend business compare to weekdays?**
```sql
SELECT 
    CASE 
        WHEN weekday IN ('Sat', 'Sun') THEN 'Weekend'
        ELSE 'Weekday'
    END AS day_type,
    SUM(money) AS total_revenue,
    COUNT(*) AS total_orders
FROM coffee_sales
GROUP BY day_type;
```
**Answer:**

<img width="395" height="112" alt="image" src="https://github.com/user-attachments/assets/dda6416c-46b9-4637-9188-3556c88fe9b6" />

**7. How has our revenue changed month by month?**

```sql
SELECT
	month_name,
	SUM(money) AS monthly_revenue
FROM
	coffee_sales
GROUP BY
	month_name,monthsort
ORDER BY
	monthsort ASC
```
**Answer:**

<img width="333" height="421" alt="image" src="https://github.com/user-attachments/assets/a5d6728b-07dd-46c5-835c-7ac7df24f11c" />

***
### 📊 Executive Summary
**8.What are our key business metrics?**
```sql
SELECT
	count(*) AS total_orders,
	SUM(money) AS total_revenue,
	ROUND(AVG(money),2) AS avg_order_value,
	count(DISTINCT date) AS business_days,
	ROUND(SUM(money)/count(DISTINCT date),2) AS avg_daily_revenue
FROM
	coffee_sales
```
**Answer:**

<img width="738" height="74" alt="image" src="https://github.com/user-attachments/assets/55258902-a0c8-42ab-8016-7059f7262b98" />


## Key Findings
Summary of the most important insights discovered through the analysis.

## Business Recommendations
Actionable recommendations based on the SQL analysis results.

## Tools Used
- PostgreSQL
- Power BI


## Files in This Repository
- [Raw Dataset](powerbi/dax_calculations.md)
- `sql_queries.sql`: All SQL queries used in the analysis
- `analysis_results.md`: Summary of findings
