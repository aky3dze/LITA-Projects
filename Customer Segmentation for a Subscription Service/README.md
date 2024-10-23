# Customer-Segmentation-for-a-Subscription-Service
<p align="center">
<img src="https://github.com/user-attachments/assets/e8e96962-dabb-4771-ac6d-124b05ed68ed" width="600" height="400">

  
- [Overview](overview)
- [Objectives](objectives)
- [Data Source and Overview](data_source_and_overview)
- [Tools used](tools_used)
- [Data Cleaning and Preparation](Data_Cleaning_and_preparation)
- [Exploratory data analysis](Exploratory_data_analysis)
- [Data visualization](Data_visualization)


### Overview
---
For this project, I will analyse customer data for a subscription service to identify segments and trends. The report outlines key insights derived from customer subscription data using Microsoft Excel, SQL queries, and PowerBi. The analysis focuses on various aspects of customer behaviour, such as subscription retention, cancellations, revenue generation, and regional differences.


### Objectives
---
The analysis aims to:
- Understand customer behaviour
- Track different subscription types
- Identify key trends in cancellations and renewals
- Calculate key business metrics such as customer retention, churn, and revenue
- Provide actionable insights that could help optimise customer engagement strategies
- The final deliverable will be a Power BI dashboard that presents my analysis. 


### Data Source and Overview
---
This data was obtained from the Ladies in Tech Africa (LITA) capstone project file. The data is structured in a single table with the following attributes:

- _**CustomerID**_ – Unique identifier for customers.
- _**CustomerName**_ – Name of the customers.
- **_Region_** – The region where the customer is located.
- _**SubscriptionType**_ – Type of subscription (e.g., Basic, Premium, Standard).
- _**SubscriptionStart**_ – Date when the subscription started.
- _**SubscriptionEnd**_ – Date when the subscription ended.
- _**Canceled**_ – Whether the subscription was canceled (True/False).
- **_Revenue_** – Revenue generated from the customer.


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
---retrieves all subscription data
select *
from sub
````

**total number of customers from each region**
````sql
select Region, count(CustomerID) as TotalCustomers
from sub
group by Region
````

**most popular subscription type by the number of customers**
````sql
select top 1 SubscriptionType, COUNT(CustomerID) AS CustomerCount
from sub
group by SubscriptionType
````

**customers who cancelled their subscription within 6 months**
````sql 
select CustomerID, CustomerName, SubscriptionStart, SubscriptionEnd 
from sub
where Canceled = 1 and DATEDIFF(month, SubscriptionStart, SubscriptionEnd)  <=6
````


**calculate the average subscription duration for all customers**
````sql
--in days
select Avg(DATEDIFF(day, SubscriptionStart, SubscriptionEnd)) as AvgSubscriptionDurationDays
from sub

--in months
select Avg(DATEDIFF(month, SubscriptionStart, SubscriptionEnd)) as AvgSubscriptionDurationMonths
from sub
````

**customers with subscriptions longer than 12 months**
````sql 
select CustomerID, CustomerName, SubscriptionStart, SubscriptionEnd 
from sub
where DATEDIFF(month, SubscriptionStart, SubscriptionEnd) >12
````

**total revenue by subscription type**
````sql
select SubscriptionType, sum(Revenue) as TotalRevenue 
from sub
group by SubscriptionType
````


**top 3 regions by subscription cancellations** 
````sql
select top 3 Region, count(CustomerID) as CanceledSubscriptions 
from Sub
where Canceled = 1
group by Region 
order by CanceledSubscriptions desc
````


**total number of active and canceled subscriptions** 
````sql
-- Active subscriptions are those where Canceled = 0 (False).
-- Canceled subscriptions are those where Canceled = 1 (True).

Select 
    sum(case when Canceled = 0 then 1 else 0 end) as ActiveSubscriptions,
    sum(case when Canceled = 1 then 1 else 0 end) as CanceledSubscriptions
from sub
````

### Data visualization
---


