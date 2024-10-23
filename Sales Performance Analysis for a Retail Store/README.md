# Sales-Performance-Analysis-for-a-Retail-Store-
<p align="center">
<img src="https://github.com/user-attachments/assets/5a96f4ac-66f4-4013-9162-25b68efb0daf" width="800" height="400">



- [Description](description)
- [Objectives](objectives)
- [Data Source](data_source)

### Description
---
For this project, I will analyse the sales performance of a retail store. I will explore sales data to uncover key insights such as top-selling products, regional performance, and monthly sales trends. I aim to produce an interactive Power BI dashboard that highlights these findings.


### Objectives
---

### Data Source
---
LITA

### Tools used
---
- Microsoft Excel [Download Here](https://www.microsoft.com/es-es/)
  1. for data cleaning
  2. for analysis
     
- SQL for extracting key insights
- PowerBi for visualization
- Github for portfolio building

### Data Cleaning and Preparation
---
data loading and inspection
handling missing variables
data cleaning and formating

### Exploratory data analysis
---
````sql
--Product renamed as Item

--retrieves entire table
select *
from sales
````

**total sales for each product category**
````sql
select Item, sum(Sales) as total_sales 
from sales
group by Item
````

**number of sales transactions in each region** 
````sql
select Region, count(OrderDate) as total_transactions 
from sales
group by Region
````

**highest-selling product by total sales value**
````sql
select  top 1 Item, sum(Sales) as highest_selling 
from sales
group by Item
````

**total revenue per product**
````sql
select Item, sum([Quantity]*[UnitPrice]) as total_sales 
from sales
group by Item
````

**monthly sales totals for the current year**
````sql 
select year(OrderDate) as sales_year, month(OrderDate) as sales_month, sum(Sales) AS total_sales
from sales
group by year(OrderDate), month(OrderDate)
having year(OrderDate) = '2024'
order by month(OrderDate)
````

**top 5 customers by total purchase amount**
````sql
select  top 5 Customer_Id, sum([Quantity]*[UnitPrice]) as highest_selling 
from sales
group by Customer_Id
order by highest_selling desc
````

**percentage of total sales contributed by each region** 
````sql
select Region, sum(Sales*100.0)/(select sum(Sales) from sales) as total_percent
from sales
group by Region
order by total_percent desc
````


**products with no sales in the last quarter**
````sql
select distinct Item as not_sold
from sales
where Item not in (
select Item
from sales
where OrderDate between '2023-10-01' and '2023-12-31'
group by Item
)
````


### Data visualization
---


