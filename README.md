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





