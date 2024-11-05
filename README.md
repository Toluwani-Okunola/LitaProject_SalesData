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
These are the excel formular i used to get the avearage sales per product and total reveue per region

![S Formular Result](https://github.com/user-attachments/assets/7c0ea4bc-cf20-42aa-a5e7-2e45e36606ee)

These are the codes I wrote to query the data
```
SELECT * FROM [dbo].[Sales Data]
```
1. Retrieve the total sales for each product category
 ```
   SELECT Product, SUM(Sales) AS TotalSales FROM [dbo].[Sales Data]
    GROUP BY Product
 ```
![sales data q1](https://github.com/user-attachments/assets/297f4c6c-b8b3-44d8-8989-978889afb85d)

2. Find the numbers of sales transaction in each region
   ```
   SELECT Region, COUNT(OrderID) AS No_of_SalesTransaction FROM [dbo].[Sales Data]
    GROUP BY Region
   ```
 ![sales data q2](https://github.com/user-attachments/assets/25d63991-79d8-4a90-adc2-a1522a3fa96d)

3. Find the highest-selling product by total sales value
   ```
    SELECT TOP 1 Product, SUM(Sales) AS HighestSelling FROM [dbo].[Sales Data]
    GROUP BY Product
    ORDER BY 2 desc
   ```
![sales data q3](https://github.com/user-attachments/assets/b9b2999f-538e-423f-9114-9689be86413b)

4. calculate total revenue per product.
  ```
  Select Product, SUM(Sales) AS TotalRevenue FROM [dbo].[Sales Data]
  GROUP BY Product
```
![sales data q4](https://github.com/user-attachments/assets/0c90d3d5-7b4e-4cbd-86c8-0a7f56465d80)

5. Calculate monthly sales totals for the current year.
```
SELECT OrderDate, SUM(Sales) AS MonthlySales_Total FROM [dbo].[Sales Data]
WHERE Orderdate between '2024-01-01' and '2024-12-31'
GROUP BY OrderDate
ORDER by OrderDate
```
![sales data q5](https://github.com/user-attachments/assets/7155ce8f-3abe-4820-9654-76c7fa13676f)
6. find the top 5 customers by total purchase amount.
```
SELECT TOP 5 (CustomerID),SUM(Sales) AS TotalPurchase FROM [dbo].[Sales Data]
GROUP BY CustomerID
ORDER BY TotalPurchase desc
```
![sales data q6](https://github.com/user-attachments/assets/fae23c34-8f9b-452d-bd52-1277020ece43)
7. calculate the percentage of total sales contributed by each region.
```
WITH Region AS (
SELECT Region, SUM(Sales) AS Sales FROM [dbo].[Sales Data]
GROUP BY Region)
SELECT Region, (Sales * 100.0 / (SELECT SUM (Sales) FROM [dbo].[Sales Data])) AS SalesPercentage
From Region
```
![sales data q7](https://github.com/user-attachments/assets/9d5c42d5-c61f-4ef6-a1db-6275c61ac976)
8. identify products with no sales in the last quarter.
```
SELECT Product FROM [dbo].[Sales Data]
WHERE Product NOT IN (SELECT Product FROM [dbo].[Sales Data]
Where OrderDate BETWEEN '2024-07-01' AND '2024-09-30')
GROUP BY Product
```
![sales data q8](https://github.com/user-attachments/assets/7f97e855-6f95-4b7b-8e9f-a3427a73c5f5)

### Visual Analysis 
Data summary using pivot table
![Sales Data](https://github.com/user-attachments/assets/584cff12-8d7e-4256-a3bc-72fb3bb49507)
![sales data 1](https://github.com/user-attachments/assets/f67e732a-57b6-474b-9be3-bfbe48da8e34)
![sales data 2](https://github.com/user-attachments/assets/df2b3cb7-f203-455d-8811-e99ccc735c90)
![sales data 3](https://github.com/user-attachments/assets/68a3f8e5-c49d-4ccd-bdfb-929ee4622606)

Data Visualization
![sales visuals](https://github.com/user-attachments/assets/64458c48-8b2d-43df-9290-e1e4cbd8e192)
![sales visual 1](https://github.com/user-attachments/assets/086e9ec4-f6b2-4e92-baca-0742ab75ccb1)
![sales visual 2](https://github.com/user-attachments/assets/e57cd2c4-44b2-458c-95bb-15a70b6b4d14)
![sales visual 3](https://github.com/user-attachments/assets/8e2df44e-3d40-4bb8-b757-df44506a1488)








### Results/Findings

### Reccommendation
1. Rotate products monthly to ensure equal market exposure.
2. Focus on Shirt, the second-best performing product by revenue and third by quantity.
3. Introduce Hat and Shirt to the South region to boost revenue.
4. Replicate the successful February marketing strategy throughout the year.

### Limitation
I created a calculated column named Sales by mltiplying unit pric and quantity. This is an important column to analysis the sales performance of the store
