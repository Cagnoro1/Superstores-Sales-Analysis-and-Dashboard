# Superstore-Sales-Analysis-and-Dashboard

![Superstore cover](https://github.com/Cagnoro1/Superstore-Sales-Analysis-and-Dashboard/assets/135088212/46b7adff-7e4d-425a-97a4-4ee4fbce7a21)


## Table of contents
- [Project Overview](#project-overview) 
- [Data Sources](#data-sources)
  - [Metadata](#metadata)
- [Tools](#tools)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results and Finding](#results-and-finding)
  - [Sales Analysis](#sales-analysis)
  - [Revenue Optimization](#revenue-optimization)
  - [Product Analysis](#product-analysis)
  - [Customer Analysis](#customer-analysis)
  - [Regional Analysis](#regional-analysis)
  - [Operational Analysis](#operational-analysis)
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


### Results and Finding

#### Sales

- Technology is the category generating the most revenue, followed closely by furniture and office supplies.
- In terms of yearly sales, 2017 stands out as the best year, while 2014 appears to be the worst.
  
#### Revenue Optimization
- Examining discounts:
  - Sales with no discount and a 0.2 discount generated the most revenue.
  - Interestingly, the discount percentage does not significantly affect the total revenue.
- Best sale month:
  - On average across the years, November is the month with the highest sales.

  
#### Product Analysis
- Top-selling products (classics) from 2014 to 2017?
   - Phones, storage, chairs, bookcases, binders, machines, and tables are the classic bestsellers.

- Profitability Analysis - Which products generate the highest profit?
  - The “Canon imageCLASS 2200 Advanced Copier” generates the highest profit.
  
- Underperforming product:
  - The “Eureka Disposable Bags for Sanitaire Vibra Groomer I Upright Vac” generates the least revenue.


#### Customer Analysis:
- Loyal customers (Top 8):
  - William Brown, Paul Prost, John Lee, Matt Abelman, Jonathan Doherty, Chloris Kastensmidt, Edward Hooks, Seth Vernon.

#### Regional Analysis:
- Total sales and profit by region:
    - East: Total sales = $678,781.24, Total profit = $91,522.78
    - South: Total sales = $391,721.91, Total profit = $46,749.43
    - West: Total sales = $725,457.82, Total profit = $108,418.45
    - Central: Total sales = $501,239.89, Total profit = $39,706.36
    

#### Operational Insights:
- Shipping methods:
  - Standard shipping is the most commonly used method.
- Discount impact on profit:
    - No discount yields the best revenue, but a 0.2 discount also generates substantial income.



### Recommendation

Based on the analysis, we recommend the following actions:
#### 1. Holiday Season Optimization:
- Consider focusing marketing efforts during the holiday season, which spans from March to November and December. This period consistently sees higher sales.
  
#### 2. Product Sales and Cost Optimization:
- The superstore should strategically manage its product offerings. Phones, chairs, storage, tables, binders, machine accessories, and copiers contribute significantly to sales revenue.
- To further optimize revenue, the superstore could negotiate deals with suppliers to reduce costs associated with these high-selling items.

#### 3. Geographic Expansion:
- California, Texas, and New York are the primary states for sales. Expanding store locations in these states could capitalize on existing demand.
- Tailoring products to the specific demographics of these regions, especially in high-traffic areas, may yield better results.

#### 4. Technology Category Investment:
- The Technology category generates substantial revenue. Investing more in tech supplies could enhance overall profitability.
  
#### 5. Consumer vs. Home Office Revenue:
- Consumers contribute more revenue than home offices. The superstore should continue to prioritize consumer-oriented products.
  

### Limitation 
  None

### References

1. Dataset 
  https://www.kaggle.com/datasets/vivek468/superstore-dataset-final 


😄 Thank you!
💻



