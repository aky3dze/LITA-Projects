# Sales Performance Analysis for a Retail Store
<p align="center">
<img src="https://github.com/user-attachments/assets/5a96f4ac-66f4-4013-9162-25b68efb0daf" width="800" height="400">



- [Project Overview](#project-overview)
- [Objectives](#objectives)
- [Data Source and Overview](#data-source-and-overview)
- [Tools and Techniques](#tools-and-techniques)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data visualization](#data-visualization)
- [Findings](#findings)
- [Conclusions and Recommendations](#conclusions-and-recommendations)
- [Limitations](#limitations)

## Project Overview 
This project provides an in-depth analysis of the sales performance of a retail store. The analysis explores sales data to uncover key insights such as top-selling products, regional performance, and monthly sales trends. The project culminates in an interactive Power BI dashboard that highlights these findings.


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
- `Product` - The type of product sold (e.g. Shirt, Shoes).
- `Region` - The geographical area where the sale occurred (North, South, etc.).
- `OrderDate` - The date when the order was placed.
- `Quantity` - The number of units ordered.
- `UnitPrice` - The price per unit of the product.

## Tools and techniques
The following tools and techniques were utilised for data processing, analysis and visualization: 
1. Microsoft Excel [Download Here](https://www.microsoft.com/es-es/) - For initial data cleaning and analysis
     
2. SQL Server - For querying and extracting key insights
  	- The following SQL techniques were used:
  	 1. Aggregate functions
  	 2. Subqueries and conditional filtering
  	     
3. Power BI - For data visualization and dashboard creation
	- The following PowerBi features were incorporated:
   	 1. Measures
   	 2. DAX functions (e.g. `CALCULATE`, `SUM`, `DIVIDE`)
   	    
- Github - To showcase this project as part of a portfolio 

## Data Cleaning and Preparation
- Data loading and inspection: The raw data was initially loaded in Excel, and checked for missing values, duplicates and consistency in data format.
- Data cleaning and formatting: This involved removing duplicates.
- Calculation of Sales using the Excel formula `= Quantity*UnitPrice`
- Loading cleaned data into SQL server and Power BI for further analysis; data types were reviewed accordingly.


## Exploratory Data Analysis (EDA)
Exploratory Data Analysis (EDA) was conducted using SQL Server to uncover key sales insights, such as top products, regional sales distribution, and monthly and daily sales trends.

### SQL Queries Used in Analysis:
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
Power BI was used to create interactive visuals that bring the data insights to life. 

![Screenshot 2024-10-30 002122](https://github.com/user-attachments/assets/d6cb9d39-6ed6-4a0c-83ff-b88796afc615)


## Findings
The findings will be broken down into two parts; Overall insights and a yearly comparison (2023 vs. 2024):

### Overall insights
---
**1. Regional sales:** Over the two-year period, total sales revenue of approximately 2 million was made from 9,921 orders. The South region generated the highest sales revenue and volume, indicating a high customer demand for products in that region. Meanwhile, the West had the lowest, suggesting an opportunity for targeted marketing to create brand awareness and product appeal there.

**2. Top-Selling Products:** Shoes generated the most revenue followed by shirts. Interestingly,  
hats led in sales volume, indicating a high turnover of a lower-priced item that customers frequently purchase.

**3. Monthly sales trends:** Peak sales and volume occurred in February probably due to seasonal demands.

**4. Daily sales trends:** Sales were highest on Tuesdays, with volume peaks on Sundays.

### A yearly comparison: 2023 vs. 2024
---
Analysing year-over-year trends gives deeper insights into understanding customer patterns:

- 2023 (January to December)
  ---
**1. Regional Sales Distribution:**  In 2023, 5952 orders were placed, raking 1 million in sales revenue. Again, the South region dominated not only in sales revenue but also in volume, while the West had the lowest revenue and volume. 

**2. Top-Selling Products:** Shirts and hats generated the most revenue followed by hats.
Shirts emerged as the product with the highest volume followed by shoes.

**3. Monthly sales trends:** Peak sales revenue occurred in February and July saw the highest sales volume.

**3. Daily sales trends:** The findings reveal Tuesdays as the busiest sales day of the work week with a high sales revenue and volume. 



- 2024 (January to August)
  ---
 **1. Regional Sales Distribution:**  In 2024, 3969 orders were placed with 996,000 in sales revenue. The South region contributed the highest revenue and the most quantity sold, while the North had the lowest sales. 

**2. Top-Selling Products:** Interestingly, customer preference seemed to have begun shifting with hats topping revenue generation followed by shoes, which had the most sales volume.

**3. Monthly sales trends:** February remained the peak month for sales revenue and volume, solidifying it as a critical period for the store.

**3. Daily sales trends:** Thursdays emerged as the day with high sales revenue, with Sunday leading in volume.
 


## Conclusions and Recommendations
The following conclusion can be drawn from the analysis:
- February had peak sales revenue across both years.
- Tuesdays and Thursdays emerged as core sales revenue days, and Sundays as the highest sales volume day.
- An equal number of orders were placed for all products in 2023.
- More orders were placed for hats and shoes in 2024 compared to the previous year.
  
The recommendations drawn from the analysis are as follows:
- Inventory for top-selling products such as shoes and hats should be increased especially during peak months.
- Marketing efforts should be increased in the West region to boost sales.
- 


## Limitations
- The dataset lacks profit details, delivery choice and customer demographics, limiting deeper insights into profit trends and customer segmentation.

😊💻
🔗[insert power bi link here]
