[README.md](https://github.com/user-attachments/files/28053645/README.md)
# ☕ Coffee Sales Analysis — SQL Project

## Project Overview

This project analyzes a coffee shop's sales data using SQL (PostgreSQL). The goal is to uncover business insights such as peak sales hours, best-selling products, revenue trends, and customer payment behavior. This project was built as part of my self-learning journey into data analytics.

---

## Dataset

- **Source:** Kaggle
- **File:** `coffee_sales.csv`
- **Total Columns:** 10

| Column | Data Type | Description |
|---|---|---|
| hour_of_day | INT | Hour the transaction occurred |
| cash_type | VARCHAR | Payment method (Cash/Card) |
| money | DECIMAL | Transaction value |
| coffee_name | VARCHAR | Name of coffee ordered |
| time_of_day | VARCHAR | Morning / Afternoon / Night |
| weekday | VARCHAR | Day of the week |
| month_name | VARCHAR | Name of the month |
| sorting_of_day | INT | Numeric sort order for days |
| sorting_of_month | INT | Numeric sort order for months |
| date | DATE | Transaction date |

---

## Tools Used

- **PostgreSQL** — Database
- **pgAdmin 4** — Query interface

---

## Business Questions & Queries

### 1. Which coffee sells the most?
```sql
SELECT coffee_name, COUNT(*) AS total_orders
FROM coffee_sales
GROUP BY coffee_name
ORDER BY total_orders DESC;
```

### 2. What is the total revenue?
```sql
SELECT SUM(money) AS total_revenue
FROM coffee_sales;
```

### 3. How many transactions were made in each month?
```sql
SELECT month_name, COUNT(*) AS total_transactions
FROM coffee_sales
GROUP BY month_name, sorting_of_month
ORDER BY sorting_of_month ASC;
```

### 4. Which hour of the day has the most sales?
```sql
SELECT hour_of_day, COUNT(*) AS top_sales
FROM coffee_sales
GROUP BY hour_of_day
ORDER BY top_sales DESC;
```

### 5. What is the most popular coffee per time of day?
```sql
SELECT time_of_day, coffee_name, COUNT(*) AS most_popular_coffee
FROM coffee_sales
GROUP BY coffee_name, time_of_day
ORDER BY 
    CASE time_of_day
        WHEN 'Morning' THEN 1
        WHEN 'Afternoon' THEN 2
        WHEN 'Night' THEN 3
    END,
    most_popular_coffee DESC;
```

### 6. Which weekday generates the most revenue?
```sql
SELECT weekday, SUM(money) AS revenue
FROM coffee_sales
GROUP BY weekday
ORDER BY revenue DESC;
```

### 7. What is the month over month revenue trend?
```sql
SELECT month_name, SUM(money) AS monthly_revenue
FROM coffee_sales
GROUP BY month_name, sorting_of_month
ORDER BY sorting_of_month ASC;
```

### 8. Which coffee has the highest average transaction value?
```sql
SELECT coffee_name, ROUND(AVG(money), 2) AS average_sales
FROM coffee_sales
GROUP BY coffee_name
ORDER BY average_sales DESC;
```

### 9. What percentage of sales came from each payment type?
```sql
SELECT cash_type, 
    ROUND(COUNT(*) * 100.0 / (SELECT COUNT(*) FROM coffee_sales), 2) AS percentage
FROM coffee_sales
GROUP BY cash_type
ORDER BY percentage DESC;
```

---

## Skills Demonstrated

- `SELECT`, `FROM`, `WHERE`, `GROUP BY`, `ORDER BY`
- Aggregate functions: `COUNT()`, `SUM()`, `AVG()`, `ROUND()`
- Subqueries
- `CASE` statements for custom sorting
- Percentage calculations
- Data filtering and ranking

---

## How to Run

1. Install [PostgreSQL](https://www.postgresql.org/) and pgAdmin 4
2. Create a new database in pgAdmin
3. Run the `CREATE TABLE` statement below to set up the table structure
4. Import `coffee_sales.csv` via pgAdmin's Import/Export tool (ensure Header is toggled ON)
5. Open and run queries from `coffee_sales_analysis.sql`

```sql
CREATE TABLE coffee_sales (
    hour_of_day INT,
    cash_type VARCHAR(50),
    money DECIMAL(10,2),
    coffee_name VARCHAR(100),
    time_of_day VARCHAR(20),
    weekday VARCHAR(20),
    month_name VARCHAR(20),
    sorting_of_day INT,
    sorting_of_month INT,
    date DATE,
    time TIME
);
```

---

## About Me

I am currently transitioning into a data analytics career and building this portfolio to demonstrate my SQL skills. This is one of several projects I am working on as part of my self-learning journey.
