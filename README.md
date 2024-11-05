# LITA_PROJECT
## PROJECT TITLE: Sales Performance Analysis for a Retail Store 
## Project Objective
---
1. The primary objective of thisproject is to analyse sales performace data for a retail shop. 
2. To identify trends
3. Access the effecftiveness of marketing strategies
4. Provide actionable insights for improvnhg sales and inventory management
   
## Data Sources
---
The primary source of Data used here is Book 1.csv. This data was gotten from the Incubator Hub (Ladies in Tech African), which I am currently taking a course with.

## Technologies Used (Tools)
---
- Microsoft Excel  [Download Here](https://WWW.Microsoft.com)
   1. data cleaning
   2. analysis
   3. visusalization
- Programing Language: SQL (Structured Query Language) [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/en-us/sql/ssms/download-sql-sever-management-studio-smss)
- Data visualization tools: Power BI [Power BI Desktop(https://powerbi.microsoft.com/en-us/downloads/)     
-Github
    1.Portfolio Building.

## Data Cleaning and preparation
---
1. Data importation
   - The data was importated after downloading an MS excel file 
   - The data was critically assessed, putting missing value and duplicate in vie
   - The cleaned data was copied to another sheet on MS excel
   - The data was changed to csv file, so it can easily be transported or imported to SQL for further analysis as requested on the project
  
## Exploratory Data Analysis (EDA)
---
The data was explored to answer the following question.
 1. On MS excel
 	-Perform an initial exploration of the sales data.
   -Use pivot tables to summarize total sales by product, region, and month.
   -Use Excel formulas to calculate metrics such as average sales per product and total revenue by region. 
   -Create any other interesting report
2. On SQL
   -retrieve the total sales for each product category. 
   -find the number of sales transactions in each region. 
   -find the highest-selling product by total sales value. 
   -calculate total revenue per product. 
   -calculate monthly sales totals for the current year.
   -find the top 5 customers by total purchase amount. 
   -calculate the percentage of total sales contributed by each region. 
   -identify products with no sales in the last quarter. 
4. On PowerBI
   -Create a dashboard that visualizes the insights found in Excel and SQL.
   N/B: The dashboard should include a sales overview, top-performing products, and regional breakdowns.

## Data Analysis
---
Code used to analyse this data 
1. Excel
 
  - To get Revenue:
   ```Excel
   Total sales * Product

  - To get Average of each product

   ```Excel
   AVERAGEIF(C:C,[@Product],I:I)
   ```

b.   Pivot table was inserted by:

    ```Excel
    - Control A to highlight the entire tabe
    - Click on Insert Tab to create a pivot table (different analysis was carried out like: Total Sales Per product, Total Sales Per Region, Total Sales Per Year, Product Per Unit Price, 
      Top selling Product Per Region, etc)
   ```

2. SQL
a. Retrieve the total sales for each product category.
   ```SQL
   select product, sum(revenue) as
   TotalSales
   from [dbo].[Book1]
   group by Product
   ```

b. find the number of sales transactions in each region. 
   ```SQL
   select Region, count(OrderID)  as
   Number_of_Transactions
   From [dbo].[Book1]
   group by Region
   ```

c. find the highest-selling product by total sales value. 
   ```SQL
   select product, sum(Revenue) as
   Total_sales
   From [dbo].[Book1]
   Group by product
   order by Total_sales desc
   ```
d. calculate total revenue per product. 
   ```SQL
   select Product, sum(Revenue) as
   Total_Revenue
   from [dbo].[Book1]
   group by product
   ```
e. calculate monthly sales totals for the current year.
   ```SQL
   select month(OrderDate) as Month,
   sum(Revenue) as
   Monthly_TotalSales
   from [dbo].[Book1]
   where Year(OrderDate) =
   Year(GETDATE()) -- Filters for the current year
   group by Month(OrderDate)
   order by Month
   ```
f. find the top 5 customers by total purchase amount. 
   ```SQL
   select top 5 Customer_Id,
   sum(Revenue) as Total_Purchase_Amount
   from [dbo].[Book1]
   group by Customer_Id
   order by Total_Purchase_Amount desc
   ```
 g. calculate the percentage of total sales contributed by each region. o identify products with no sales in the last quarter.
   ```SQL
    with Total_Sales as (
    select sum (Revenue) as
    Total_Revenue
    from [dbo].[Book1]
    )
   select
   region,
   sum(Revenue) as
   Region_TotalSales,
   (sum(Revenue) * 100.0 / (select
   Total_Revenue from Total_Sales)) AS
   Percentage_of_TotalSales
   from [dbo].[Book1]
   Group by Region
   Order by Percentage_of_TotalSales
   desc;
   ```

h. identify products with no sales in the last quarter.
   ```SQL
   select product
   from [dbo].[Book1] 
   where Product not in (
   select distinct Product
   from [dbo].[Book1]
   where OrderDate >=
   Dateadd(quarter, -1, getdate())
   )
  group by Product;
  ```
3. A dashboard was created to visualize the insight found in Excel and in PowerBI

   ## Data Visualization
   
