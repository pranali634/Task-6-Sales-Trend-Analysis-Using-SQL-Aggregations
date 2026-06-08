# Task-6-Sales-Trend-Analysis-Using-SQL-Aggregations
> **Elevate Labs Data Analyst Internship**  
> Analyzing monthly revenue and order volume from an online sales dataset using SQL aggregation functions.

---

## Repository Structure

```
Task6-Sales-Trend-Analysis/
│
├── Online Sales data.csv  # Dataset
├── Task6.sql              # All SQL queries for the task
├── Screenshotfolder       #Screenshots of all sql queries results 
└── README.md              # Project documentation

```

---

## Objective

Perform a **Sales Trend Analysis** on an online sales database by:
- Extracting and grouping sales data by **year and month**
- Calculating **total revenue** using `SUM()`
- Counting **distinct order volumes** using `COUNT(DISTINCT ...)`
- Sorting and limiting results for specific time period insights

---

## Tools & Technologies

| Tool | Purpose |
|------|---------|
| **MySQL** | Database engine used |
| **SQL** | Query language for data analysis |

---

## Dataset – `OnlineSale` Table

A custom database `OnSalesDB` was created with a single table `OnlineSale` containing **45 transaction records** spanning **January – February 2024**.

### Schema

| Column | Data Type | Description |
|--------|-----------|-------------|
| `Transaction_ID` | INT (PK) | Unique transaction identifier |
| `Order_Date` | DATE | Date of the order |
| `Product_Category` | VARCHAR(50) | Category of the product |
| `Product_Name` | VARCHAR(100) | Name of the product |
| `Units_Sold` | INT | Number of units sold |
| `Unit_Price` | DECIMAL(10,2) | Price per unit |
| `Total_Revenue` | DECIMAL(10,2) | Total revenue for the transaction |
| `Region` | VARCHAR(50) | Sales region |
| `Payment_Method` | VARCHAR(50) | Payment method used |

---

## SQL Queries & Explanations

### 1. Database & Table Setup
```sql
CREATE DATABASE OnSalesDB;
USE OnSalesDB;

CREATE TABLE OnlineSale (
    Transaction_ID INT PRIMARY KEY,
    Order_Date DATE,
    Product_Category VARCHAR(50),
    Product_Name VARCHAR(100),
    Units_Sold INT,
    Unit_Price DECIMAL(10,2),
    Total_Revenue DECIMAL(10,2),
    Region VARCHAR(50),
    Payment_Method VARCHAR(50)
);
```
Creates the database and defines the `OnlineSale` table schema.

---

### 2. Extract Month from Order Date
```sql
SELECT MONTH(Order_Date) FROM OnlineSale;
```
Extracts the **month number** from each order's date.

---

### 3. Group by Year and Month *(Monthly Trend)*
```sql
SELECT YEAR(Order_Date), MONTH(Order_Date)
FROM OnlineSale
GROUP BY YEAR(Order_Date), MONTH(Order_Date);
```
Groups all transactions by **year and month** to identify distinct time periods in the dataset.

---

### 4. Total Revenue
```sql
SELECT SUM(Total_Revenue) FROM OnlineSale;
```
Calculates the **overall total revenue** across all transactions.

---

### 5. Distinct Order Volume
```sql
SELECT COUNT(DISTINCT Transaction_ID) FROM OnlineSale;
```
Counts the **total number of unique orders** placed.

---

### 6. Transactions Sorted by Date
```sql
SELECT Transaction_ID, Order_Date, Total_Revenue
FROM OnlineSale
ORDER BY Order_Date;
```
Returns all transactions sorted **chronologically** by order date.

---

### 7. Top 10 Earliest Transactions
```sql
SELECT TOP 10 Transaction_ID, Order_Date, Total_Revenue
FROM OnlineSale
ORDER BY Order_Date ASC;
```
Retrieves the **first 10 transactions** by date — useful for early-period analysis.

---

## Key Results

| Metric | Value |
|--------|-------|
| **Total Transactions** | 45 |
| **Date Range** | Jan 1, 2024 – Feb 14, 2024 |
| **Total Revenue** | *(Run `SUM(Total_Revenue)` query)* |
| **Regions Covered** | North America, Europe, Asia |
| **Payment Methods** | Credit Card, PayPal, Debit Card |
| **Product Categories** | Electronics, Clothing, Books, Sports, Beauty Products, Home Appliances |

---

## Key Learnings

- Used `MONTH()` and `YEAR()` functions to extract date components for time-based grouping
- Applied `GROUP BY` on multiple columns (`YEAR`, `MONTH`) for monthly trend analysis
- Used `SUM()` for revenue aggregation and `COUNT(DISTINCT ...)` for unique order volume
- Used `ORDER BY` with `ASC`/`DESC` for chronological sorting
- Used `TOP 10` (MySQL equivalent: `LIMIT 10`) to restrict result sets for focused analysis

---

## Author
**Pranali Ranjane**
**Internship:** Elevate Labs – Data Analyst Internship  
**Task:** Task 6 – Sales Trend Analysis Using Aggregations
