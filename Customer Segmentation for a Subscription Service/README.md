# Customer-Segmentation-for-a-Subscription-Service

- [Description](description)
- [Objectives](objectives)
- [Data Source](data_source)

### Description
---
For this project, I will analyse customer data for a subscription service to identify segments and trends. I aim to understand customer behaviour, track different subscription types, and identify key trends in cancellations and renewals. The final deliverable will be a Power BI dashboard that presents my analysis.


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
select SubscriptionType, SUM(Revenue) AS TotalRevenue 
from sub
group by SubscriptionType
````


**top 3 regions by subscription cancellations** 
````sql
select top 3 Region, COUNT(CustomerID) AS CanceledSubscriptions 
from Sub
where Canceled = 1
group by Region 
order by CanceledSubscriptions desc
````


**find the total number of active and canceled subscriptions** 
````sql
Select 
    sum(case when Canceled = 0 then 1 else 0 end) as ActiveSubscriptions,
    sum(case when Canceled = 1 then 1 else 0 end) as CanceledSubscriptions
from sub
````

### Data visualization
---


