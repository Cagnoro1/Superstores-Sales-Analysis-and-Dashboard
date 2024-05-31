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
The project involves the analysis of sales data from the Superstore database. The data ranged from 2014 to 2017. This project aims to analyze the Superstore sales database in depth. This project is divided into two parts: 
1) The customer segmentation Analysis  using SQL.
2) The visualization Dashboard on Tableau.


## Data Source
This data came from Kaggle:
https://www.kaggle.com/datasets/vivek468/superstore-dataset-final


### Metadata
Row ID => Unique ID for each row.
Order ID => Unique Order ID for each Customer.
Order Date => Order Date of the product.
Ship Date => Shipping Date of the Product.
Ship Mode=> Shipping Mode specified by the Customer.
Customer ID => Unique ID to identify each Customer.
Customer Name => Name of the Customer.
Segment => The segment where the Customer belongs.
Country => Country of residence of the Customer.
City => City of residence of the Customer.
State => State of residence of the Customer.
Postal Code => Postal Code of every Customer.
Region => Region where the Customer belongs.
Product ID => Unique ID of the Product.
Category => Category of the product ordered.
Sub-Category => Sub-Category of the product ordered.
Product Name => Name of the Product
Sales => Sales of the Product.
Quantity => Quantity of the Product.
Discount => Discount provided.
Profit => Profit/Loss incurred.


## Tools
Microsoft SQL Server (SQL) -  used as the primary tool for data analysis. SQL queries were written and executed to extract, manipulate, and analyze the data stored in the "Superstore" table (database).
Azure Data Studio - used to host MSSQL
Microsoft Excel - Data cleaning, Data Analysis
Tableau - Create Dashboard Report


## Data Cleaning and Preparation
For the most part, this data did not need much cleaning. Microsoft Excel  was used to separate "Order Date" by Day Month and Year.


## Exploratory Data Analysis
Explored the sales data to answer key questions, such as:

1) What are the top-selling products overall?
2) What are the top-selling products by Category and subcategory?
3) Profitability Analysis - Which products generate the highest profit?
4) Customer Segmentation - What are the main customer segments?
5) Regional Performance - What are the total sales and profit by Region?
6) Shipping Analysis- What are the most commonly used shipping models?
7) Discount Impact - What effect do discounts have on profit?
8) Time Trends - Are there any seasonal trends in sales or profit?
9) Customer Loyalty - List the loyal customers.
10) Product Portfolio Optimization - What are the underperforming products?

 In-depth analysis
 a) Let's start by grouping sales by category
 b) Let's group sales across the years
 c) Let's group sales across the years for each category 2015 has the least revenue, let's see in which month they operated in 2015
 d) Let's see with which discount they generate the more revenue
 e) What was the best month for sales in a specific year, and how much was earned in that month?
 f) What type of products do they sell the most (classic) from 2014 to 2017?
 g) Who are our best customers?





