# Superstore-Sales-Analysis-and-Dashboard

## Table of contents
- [Project Overview](#project-overview) 
- [Data Sources](#data-sources)
- [Tools](#tools)
  - [Metadata](#metadata)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Limitation](#limitation)
- [References](#references)



## Project Overview
The project aims to analyze the key performance Indicators (KPI) of the sales data from the Superstore database to give them recommendations to increase their revenue and profit. The data ranges from 2014 to 2017. The project is divided into two parts: 
1) The customer segmentation Analysis  using SQL.
2) The visualization Dashboard on Tableau.


## Data Source
This data came from Kaggle:
https://www.kaggle.com/datasets/vivek468/superstore-dataset-final


### Metadata
- Row ID => Unique ID for each row.
- Order ID => Unique Order ID for each Customer.
- Order Date => Order Date of the product.
- Ship Date => Shipping Date of the Product.
- Ship Mode=> Shipping Mode specified by the Customer.
- Customer ID => Unique ID to identify each Customer.
- Customer Name => Name of the Customer.
- Segment => The segment where the Customer belongs.
- Country => Country of residence of the Customer.
- City => City of residence of the Customer.
- State => State of residence of the Customer.
- Postal Code => Postal Code of every Customer.
- Region => Region where the Customer belongs.
- Product ID => Unique ID of the Product.
- Category => Category of the product ordered.
- Sub-Category => Sub-Category of the product ordered.
- Product Name => Name of the Product
- Sales => Sales of the Product.
- Quantity => Quantity of the Product.
- Discount => Discount provided.
- Profit => Profit/Loss incurred.


## Tools
* Microsoft SQL Server (SQL) -  used as the primary tool for data analysis. SQL queries were written and executed to extract, manipulate, and analyze the data stored in the "Superstore" table (database).
* Azure Data Studio - used to host MSSQL
* Microsoft Excel - Data cleaning, Data Analysis
* Tableau - Create Dashboard Report

## Data Cleaning and Preparation
Microsoft Excel was used to clean this data. Here is what was done:
- Added filters to each column
- Separated "Order Date" by Day Month and Year.

## Exploratory Data Analysis
Explored the sales data to answer key questions, such as:

1) Let's start by grouping sales by category.
2) Let's group sales across the years.
3) Let's group sales across the years for each category.
4) Let's see in which month they operated the least.
5) Let's see with which discount they generate the more revenue.
6) What was the best month for sales in a specific year, and how much was earned in that month?
7) What type of products do they sell the most (classic) from 2014 to 2017?
8) Who are our best customers?
9) What are the top-selling products overall?
10) What are the top-selling products by Category and subcategory?
11) Profitability Analysis - Which products generate the highest profit?
12) Customer Segmentation - What are the main customer segments?
13) Regional Performance - What are the total sales and profit by Region?
14) Shipping Analysis- What are the most commonly used shipping models?
15) Discount Impact - What effect do discounts have on profit?
16) Time Trends - Are there any seasonal trends in sales or profit?
17) Customer Loyalty - List the loyal customers.
18) Product Portfolio Optimization - What are the underperforming products?


### Data Analysis 
  Code/features worked with
  
```SQL
-- Data Analysis SQL Queries for Superstore 

-- Inspecting data
SELECT * FROM dbo.Superstore

-- Analysis 

-- Let's start by grouping sales by category
SELECT Category, SUM(Sales) AS Revenue
FROM Superstore
GROUP BY Category;

-- Let's group sales across the years
SELECT O_Year, SUM(Sales) AS Revenue
FROM Superstore
GROUP BY O_Year;

--- RESULT: 2017 seems to be the best year of sales and 2014 seems to be the worst

--  Let's group sales across the years for each category
SELECT O_Year, Category, SUM(Sales) AS Revenue
FROM Superstore
GROUP BY O_Year, Category
ORDER BY O_Year, Category;

-- Since 2015 has the least revenue, let's see in which month they operated in 2015
SELECT DISTINCT O_Month
FROM Superstore
WHERE O_Year = 2015
ORDER BY O_Month;

-- Let's see with which discount they generate the more revenue
SELECT Discount, SUM(Sales) AS Total_Revenue
FROM Superstore
GROUP BY Discount
ORDER BY Total_Revenue DESC;

-- What was the best month for sales in a specific year, and how much was earned in that month?
SELECT O_Month, O_Year, SUM(Sales) AS Total_Sales
FROM Superstore
WHERE O_Year = 2016 --  change year to see the rest
GROUP BY O_Year, O_Month
ORDER BY Total_Sales DESC ;

--- Results:  November seems to be the month with the most sales on average across the years. 


-- What type of products do they sell the most (classic) from 2014 to 2017?
SELECT O_Year, Category, Sub_Category, SUM(Sales) AS Revenue, COUNT(Quantity) AS Quantity
FROM Superstore
WHERE O_Month = 11 -- for November across the years
GROUP BY O_Year, Category, Sub_Category
ORDER BY O_Year, Revenue DESC;


--- Here it's 2017 November but it could be changed
SELECT O_Year, Category, Sub_Category, SUM(Sales) AS Revenue, COUNT(Quantity) AS Quantity
FROM Superstore
WHERE O_Month = 11 AND O_Year =  2017 -- Here it's 2017 November but it could be changed
GROUP BY O_Year, Category, Sub_Category
ORDER BY O_Year, Revenue DESC;

-- Who is our best customer?
SELECT 
        Customer_Name,
        sum(sales) AS Monetary_value,
        AVG(sales) AS Avg_Monetary_value,
        COUNT(customer_ID) AS Frequency,
        max(order_date) AS Last_Order_Date,
        DATEDIFF (day, max (Order_Date),  GETDATE()) AS Recency
        FROM Superstore
        Group by Customer_Name
        ORDER BY Monetary_value DESC ;

-- What are the top-selling products overall?
SELECT Product_Name,
SUM(Sales) As Total_Sales
from Superstore
Group By Product_Name
Order by Total_Sales DESC;

-- What are the top-selling products by Category and subcategory?
SELECT Category, Sub_Category, Product_Name,
SUM(Sales) AS Total_Sales
FROM Superstore
Group By Category, Sub_Category, Product_Name
Order by Category, Sub_Category, Total_Sales DESC ;

-- Profitability Analysis - Which products generate the highest profit?
SELECT Product_Name,
SUM(Profit) AS Total_Profit,
AVG(Profit) AS Avg_Profit,
COUNT(customer_ID) AS Frequency
From  Superstore
Group By Product_Name
Order By Total_Profit DESC;

-- Customer Segmentation - What are the main customer segments?
SELECT Segment,
SUM(Sales) AS Total_Sales ,
SUM(Profit) As Total_Profit
From  Superstore
Group By Segment;

-- Regional Performance - What are the total sales and profit by Region?
SELECT Region,
SUM(Sales) AS Total_Sales ,
SUM(Profit) As Total_Profit
From  Superstore
Group By Region;

-- Shipping Analysis- What are the most commonly used shipping models?
SELECT Ship_Mode,
COUNT(*) AS Frequency 
From  Superstore
Group By Ship_Mode
Order By Frequency DESC;

-- Discount Impact - What effect do discounts have on profit?
SELECT Discount,
AVG(Sales) AS Average_Sales,
AVG(Profit) AS Average_Profit 
From  Superstore
Group By Discount
Order By Discount;

-- Time Trends - Are there any seasonal trends in sales or profit?
SELECT
MONTH (Order_Date) AS Month,
YEAR(Order_Date) AS Year,
SUM(Sales) AS Sales
From  Superstore
Group By Year (Order_Date),
MONTH (Order_Date)
Order By Month, Year ;

-- Customer Loyalty - List the loyal customers.
SELECT Customer_ID, Customer_Name,
COUNT(*) AS Purchase_Count
From  Superstore
Group By Customer_ID, Customer_Name
HAVING COUNT(*)>1
ORDER BY Purchase_Count DESC ;

-- Product Portfolio Optimization - What are the underperforming products?
SELECT Product_Name,
SUM(Sales) AS Total_Sales,
AVG(Sales) AS Avg_Sales,
COUNT(customer_ID) AS Frequency
From  Superstore
Group By Product_Name
ORDER BY Total_Sales ASC ;


```


