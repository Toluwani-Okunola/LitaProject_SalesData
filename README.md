# LitaProject_SalesData

## Sales Data

### Project Overview
This data analysis project aims to provide insights into the sales performance of a retail store over the past and current year. By analysising various aspect of the data, we seek to identify (top selling product, product performance, regional performance and monthly sales trend, make data driven reccommendation and gain deeper understanding of the store performance

### Data Source
The primary dataset used for this analysis is the "sales data.csv" file containing detailed information about each sales made by the store. This was provided by the Incubator Hub.

### Tool Used
- Excel: 
  - Data Cleaning and Preparation
  - Data Analysis
- SQL: Structured Query Language for Querying of Data
- Power BI:
  - Data Visualization
  - Creating Report

### Data Cleaning and Preparation
In the initial stage, I performed the following task:
1. Data Loading and Inspection
2. Data Cleaning and Formating

### Exploratory Data Analysis
EDA involves exploring the sales data to answer key questions, such as;
  1. What is the overall sales trends?
  2. Which products are top sellers?
  3. What is the regional performance?
  4. What is the monthly sales trends?

### Data Analysis
These are the codes I wrote to query the data
1. Retrieve the total sales for each product category
 ```
   SELECT Product, SUM(Sales) AS TotalSales FROM [dbo].[Sales Data]
    GROUP BY Product
   ```
2. Find the numbers of sales transaction in each region
   ```
   SELECT Region, COUNT(OrderID) AS No_of_SalesTransaction FROM [dbo].[Sales Data]
    GROUP BY Region
   ```
3. Find the highest-selling product by total sales value
   ```
    SELECT TOP 1 Product, SUM(Sales) AS HighestSelling FROM [dbo].[Sales Data]
    GROUP BY Product
    ORDER BY 2 desc
   ```
4. calculate total revenue per product.
  ```
  Select Product, SUM(Sales) AS TotalRevenue FROM [dbo].[Sales Data]
  GROUP BY Product
```
5. Calculate monthly sales totals for the current year.
```
SELECT OrderDate, SUM(Sales) AS MonthlySales_Total FROM [dbo].[Sales Data]
WHERE Orderdate between '2024-01-01' and '2024-12-31'
GROUP BY OrderDate
ORDER by OrderDate
```
6. find the top 5 customers by total purchase amount.
```
SELECT TOP 5 (CustomerID),SUM(Sales) AS TotalPurchase FROM [dbo].[Sales Data]
GROUP BY CustomerID
ORDER BY TotalPurchase desc
```
7. calculate the percentage of total sales contributed by each region.
```
WITH Region AS (
SELECT Region, SUM(Sales) AS Sales FROM [dbo].[Sales Data]
GROUP BY Region)
SELECT Region, (Sales * 100.0 / (SELECT SUM (Sales) FROM [dbo].[Sales Data])) AS SalesPercentage
From Region
```
8. identify products with no sales in the last quarter.
```
SELECT Product FROM [dbo].[Sales Data]
WHERE Product NOT IN (SELECT Product FROM [dbo].[Sales Data]
Where OrderDate BETWEEN '2024-07-01' AND '2024-09-30')
GROUP BY Product
```

### Results/Findings

### Reccommendation

### Limitation
I created a calculated column named Sales by mltiplying unit pric and quantity. This is an important column to analysis the sales performance of the store
