# Walmart Sales Data Analysis

## About

This project explores Walmart sales data to analyze top-performing branches and products, sales trends, and customer behavior. The goal is to identify factors affecting sales and optimize sales strategies. The dataset was obtained from the [Kaggle Walmart Sales Forecasting Competition](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting).

> "In this competition, participants are provided with historical sales data for 45 Walmart stores across different regions. Each store has multiple departments, and participants must forecast department-wise sales. Selected holiday markdown events are included, impacting sales unpredictably." [source](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting)

## Project Objectives

The primary objective is to gain insights into Walmart sales data to understand the different factors affecting sales across various branches.

## Dataset Overview

The dataset consists of sales transactions from three Walmart branches located in Mandalay, Yangon, and Naypyitaw. It contains 17 columns and 1000 rows:

| Column                  | Description                             | Data Type      |
|-------------------------|-----------------------------------------|---------------|
| invoice_id              | Invoice identifier                      | VARCHAR(30)   |
| branch                  | Branch location                         | VARCHAR(5)    |
| city                    | City of the branch                      | VARCHAR(30)   |
| customer_type           | Customer category                       | VARCHAR(30)   |
| gender                  | Customer gender                         | VARCHAR(10)   |
| product_line            | Product category                        | VARCHAR(100)  |
| unit_price              | Price per unit                          | DECIMAL(10,2) |
| quantity                | Quantity purchased                      | INT           |
| VAT                     | Value Added Tax                         | FLOAT(6,4)    |
| total                   | Total purchase cost                     | DECIMAL(10,2) |
| date                    | Purchase date                           | DATE          |
| time                    | Purchase time                           | TIMESTAMP     |
| payment_method          | Payment method used                     | VARCHAR(30)   |
| cogs                    | Cost of Goods Sold                      | DECIMAL(10,2) |
| gross_margin_percentage | Profit margin percentage                | FLOAT(11,9)   |
| gross_income            | Gross profit                            | DECIMAL(10,2) |
| rating                  | Customer rating                         | FLOAT(2,1)    |

## Analysis Goals

### 1. Product Analysis
- Identify top-performing product lines.
- Determine product lines that require improvement.

### 2. Sales Analysis
- Analyze sales trends across product lines.
- Measure sales strategy effectiveness and suggest improvements.

### 3. Customer Analysis
- Identify customer segments and their purchasing behaviors.
- Analyze the profitability of different customer segments.

## Approach

### 1. Data Wrangling
- Inspect data for NULL values and missing entries.
- Clean data and replace missing values where necessary.
- Store the cleaned dataset in a structured database.

### 2. Feature Engineering
- Add `time_of_day` to classify purchases into Morning, Afternoon, and Evening.
- Extract `day_name` to analyze busiest days of the week.
- Extract `month_name` to determine peak sales months.

### 3. Exploratory Data Analysis (EDA)
- Perform data visualization to identify trends and insights.
- Answer business questions through statistical analysis.

### 4. Conclusion & Recommendations
- Provide data-driven recommendations for sales and marketing improvements.

## Business Questions to Answer

### General
1. How many unique cities are represented in the dataset?
2. Which city is each branch located in?

### Product Insights
1. How many unique product lines exist?
2. What is the most common payment method?
3. Which product line generates the highest sales?
4. What is the total monthly revenue?
5. Which month had the highest COGS?
6. Which product line contributed the most revenue?
7. Which city has the highest revenue?
8. Which product line has the highest VAT?
9. Classify each product line as "Good" or "Bad" based on average sales.
10. Which branch sold more products than the average quantity sold?
11. What is the most popular product line by gender?
12. What is the average rating of each product line?

### Sales Insights
1. Number of sales made at different times of the day per weekday.
2. Which customer type generates the most revenue?
3. Which city has the highest VAT percentage?
4. Which customer type pays the most VAT?

### Customer Insights
1. How many unique customer types exist?
2. How many unique payment methods are used?
3. What is the most common customer type?
4. Which customer type purchases the most?
5. What is the gender distribution of customers?
6. How does gender distribution vary per branch?
7. When do customers leave the most ratings?
8. When do customers leave the most ratings per branch?
9. Which day has the highest average ratings?
10. Which branch has the highest average ratings per weekday?

## Revenue and Profit Calculations

### Formulas Used:
- **COGS (Cost of Goods Sold):**
  \[ COGS = \text{unit price} \times \text{quantity} \]
- **VAT Calculation:**
  \[ VAT = 5\% \times COGS \]
- **Total Sales Calculation:**
  \[ \text{Total (Gross Sales)} = VAT + COGS \]
- **Gross Profit Calculation:**
  \[ \text{Gross Profit} = \text{Total Sales} - COGS \]
- **Gross Margin Percentage:**
  \[ \text{Gross Margin} = \frac{\text{Gross Profit}}{\text{Total Revenue}} \]

### Example Calculation:
Given:
- **Unit Price:** $45.79$
- **Quantity:** $7$

1. **COGS:**
   \[ 45.79 \times 7 = 320.53 \]
2. **VAT Calculation:**
   \[ 5\% \times 320.53 = 16.0265 \]
3. **Total Sales Calculation:**
   \[ 320.53 + 16.0265 = 336.5565 \]
4. **Gross Margin Percentage:**
   \[ \frac{16.0265}{336.5565} \approx 4.76\% \]

## SQL Database Setup

```sql
-- Create database
CREATE DATABASE IF NOT EXISTS walmartSales;

-- Create table
CREATE TABLE IF NOT EXISTS sales (
    invoice_id VARCHAR(30) NOT NULL PRIMARY KEY,
    branch VARCHAR(5) NOT NULL,
    city VARCHAR(30) NOT NULL,
    customer_type VARCHAR(30) NOT NULL,
    gender VARCHAR(30) NOT NULL,
    product_line VARCHAR(100) NOT NULL,
    unit_price DECIMAL(10,2) NOT NULL,
    quantity INT NOT NULL,
    tax_pct FLOAT(6,4) NOT NULL,
    total DECIMAL(12,4) NOT NULL,
    date DATETIME NOT NULL,
    time TIME NOT NULL,
    payment VARCHAR(15) NOT NULL,
    cogs DECIMAL(10,2) NOT NULL,
    gross_margin_pct FLOAT(11,9),
    gross_income DECIMAL(12,4),
    rating FLOAT(2,1)
);
```

For complete SQL queries and analysis, refer to the https://github.com/Ncheruiyot/Walmart-Sales-Data-Analysis/commit/30399b3167d32cc02c8548becf6fbe712da5d93c file.
