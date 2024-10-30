# Sales Performance Analysis for a Retail Store
<p align="center">
<img src="https://github.com/user-attachments/assets/5a96f4ac-66f4-4013-9162-25b68efb0daf" width="800" height="400">



- [Project Overview](#project-overview)
- [Objectives](#objectives)
- [Data Source and Overview](#data-source-and-overview)
- [Tools](#tools)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data visualization](#data-visualization)
- [Findings](#findings)
- [Conclusions and Recommendations](#conclusions-and-recommendations)
- [Limitations](#limitations)

## Project Overview 
For this project, I will analyse the sales performance of a retail store. I will explore sales data to uncover key insights such as top-selling products, regional performance, and monthly sales trends. I aim to produce an interactive Power BI dashboard that highlights these findings.


## Objectives
The main objectives of this analysis are to:
- Identify top-selling products and high-revenue-generating regions.
- Examine monthly and daily trends in sales.
- Provide insights into customer purchasing behaviour and preferences.
- Develop a dashboard to summarize findings for strategic decision-making.

## Data Source and Overview
This data was obtained from the Ladies in Tech Africa (LITA) capstone project file. It consists of a single table with the following attributes:
- `OrderID` - A unique identifier for each order.
- `Customer Id` - ID representing individual customers.
- `Product` - The type of product sold (e.g., Shirt, Shoes).
- `Region` - The geographical area where the sale occurred (North, South, etc.).
- `OrderDate` - The date when the order was placed.
- `Quantity` - The number of units ordered.
- `UnitPrice` - The price per unit of the product.

## Tools and concepts applied
The following tools and concepts were used for data processing, analysis and visualization: 
- Microsoft Excel [Download Here](https://www.microsoft.com/es-es/) - for data cleaning and initial analysis
     
- SQL server - for querying and extracting key insights
  	- The following SQL techniques were used:
  	 1. Aggregate functions
  	 2. Subqueries
  	     
- PowerBi - for data visualization and dashboard creation
	- The following PowerBi features were incorporated:
   	 1. Measures
   	 2. Calculated columns
   	 3. DAX
   	    
- Github - to showcase this project as part of a portfolio 

## Data Cleaning and Preparation
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

**1. Total sales for each product category**
````sql
select Item, sum(Sales) as total_sales 
from sales
group by Item
````
**Output**
| Item | total_sales |
| --- | --- |
| Shoes	| 613380 | 
| Jacket | 208230 |
| Hat	| 316195 |
| Socks	| 180785 |
| Shirt	| 485600 |
| Gloves | 296900 |

                                             
**2. Number of sales transactions in each region** 
````sql
select Region, count(OrderDate) as total_transactions 
from sales
group by Region
````
**Output**
| Region | total_transactions |
| --- | --- |
| North	| 2481 | 
| East | 2483 |
| South	| 2480 |
| West	| 2477 |                           


**3. Highest-selling product by total sales value**
````sql
select  top 1 Item, sum(Sales) as highest_selling 
from sales
group by Item
````

**Output**
| Item | highest_selling |
| --- | --- |
| Shoes	| 613380 | 
                                               
**4. Total revenue per product**
````sql
select Item, sum([Quantity]*[UnitPrice]) as total_sales 
from sales
group by Item
````
**Output**
| Item | total_sales |
| --- | --- |
| Shoes	| 613380 | 
| Jacket | 208230 |
| Hat	| 316195 |
| Socks	| 180785 |
| Shirt	| 485600 |
| Gloves | 296900 |

**5. Monthly sales totals for the current year**
````sql 
select year(OrderDate) as sales_year, month(OrderDate) as sales_month, sum(Sales) AS total_sales
from sales
group by year(OrderDate), month(OrderDate)
having year(OrderDate) = '2024'
order by month(OrderDate)
````
**Output**
|sales_year | sales_month | total_sales|
|----------- |-----------| -----------|
|2024     |   1      |     198400|
|2024     |   2      |    298800|
|2024    |    3     |      54780|
|2024     |   4     |      39440|
|2024     |   5      |     44640|
|2024     |   6      |     148200|
|2024     |   7     |      37200|
|2024     |   8      |     174300|

**6. Top 5 customers by total purchase amount**
````sql
select  top 5 Customer_Id, sum([Quantity]*[UnitPrice]) as highest_selling 
from sales
group by Customer_Id
order by highest_selling desc
````
**Output**
| Customer_Id | highest_selling |
| --- | --- |
| Cus1431	| 4235 | 
| Cus1495	| 4235 | 
| Cus1005	| 4235 | 
| Cus1115	| 4235 | 
| Cus1302	| 4235 | 


**7. Percentage of total sales contributed by each region** 
````sql
select Region, sum(Sales*100.0)/(select sum(Sales) from sales) as total_percent
from sales
group by Region
order by total_percent desc
````
**Output**
| Region | total_percent |
| --- | --- |
| South	| 44.158984 |
| East | 23.127281 |
| North	| 18.419011 |
| West	| 14.294723 | 


**8. Products with no sales in the last quarter**
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
**Output**
| not_sold | 
| --- |
| Hat	| 
| Shirt	|
| Shoes	|
                    
## Data visualization
![Screenshot 2024-10-30 002122](https://github.com/user-attachments/assets/d6cb9d39-6ed6-4a0c-83ff-b88796afc615)


## Findings

## Conclusions and Recommendations

## Limitations

